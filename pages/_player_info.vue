<template>
  <div class="base">

    
    <headerBar />

    <!-- main content -->
    <main>

      <section class="player-cBoard">
         <div v-if="$fetchState.pending">Fetching player</div>
         <div v-else-if="$fetchState.error">Something went wrong</div>
         

         <div v-else class="player-cBoard_img">
            <img :src="urlFor(playerInView[0].cardImage)" :alt="playerInView[0].name.toLowerCase().replace(/\s/g, '-') + '-card'">
         </div>

        <div class="player-cBoard_attr">
         {{ playerInView }}
        </div>

        <div class="player-cBoard_attr2">
          
        </div>
      </section>

      <section class="player-summary">
          <div class="palyer-summary_titl">
          </div>

          <div class="player-summary_deets">

          </div>
      </section>

    </main>

    <footerBar />
  </div>
</template>

<script>
  import client from '@/sanityConfig/index.js'
  const query = '*[_type == "fifaCard"]'

  import imageUrlBuilder from '@sanity/image-url'
  const builder = imageUrlBuilder(client)


   export default {
      name: 'PlayerDetailsPage',
      
      data() {
         return {
            playerInView: {}
         }
      },

      async asyncData({ params }) {
         //get player slug from url and merge into components 'data()'
         const player = params.player_info
         return { player }
      },

      async fetch() {
         await client.fetch(query)
            .then ((players) => {
               //use the same codeblock used to generate the url of the player's details in 'playerStatsBar.vue' 
               //to search the returned players from sanity client and find the player
               const playerInView = players.filter(player => player.slug.current === this.player);

               this.playerInView = playerInView
            })
      },

      methods: {
          urlFor(imgSrc) {
            return builder.image(imgSrc)
         }
      }
   }
</script>


