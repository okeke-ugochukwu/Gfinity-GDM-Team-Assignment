<template>
   <!-- BASE -->
  <div class="w-full min-w-max min-h-screen bg-rs-grey py-[0.05px]">
      <headerBar />

      <loader v-if="$fetchState.pending">
         <img 
            src="@/assets/imgs/RS-logo.png" alt="real-sport" 
            class="w-[100px] m-auto animate-pulse"
         />
      </loader>

      <loader v-else-if="$fetchState.error">
         Something went wrong.
      </loader>


      <!-- main content -->
      <main v-else class="w-[1024px] m-auto pt-[66px]">
         <titleBar/>
      
         <section class="player-list">
            
            <playerStatsBar 
               v-for="player in this.players" :key="player._id" 
               :player="player"
            />
         </section>

         <footerBar />
      </main>

  </div>
</template>

<script>
  import client from '@/sanityConfig/index.js'
  const query = '*[_type == "fifaCard"]'

  
  export default {
    name: 'IndexPage',

    data() {
      return {
        players: {}
      }
    },

    async fetch() {
      await client.fetch(query)
        .then ((players) => {
          this.players = players
        })
    }
  
  }
</script>


