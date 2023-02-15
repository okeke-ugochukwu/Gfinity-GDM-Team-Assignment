<template>
   <!-- APP BASE -->
  <div class="w-full min-w-max h-max bg-rs-grey">
    
    <headerBar />

    <!-- main content -->
    <main class="w-[1024px] m-auto pt-[66px]">
      <titleBar/>
      
      <section v-if="$fetchState.pending">Getting players</section>

      <section v-else class="player-list">
        
        <playerStatsBar 
          v-for="player in this.players" :key="player._id" 
          :player="player"
        />
      </section>

    </main>

    <footerBar />
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
         console.log(players)
          this.players = players
        })
    }
  
  }
</script>


