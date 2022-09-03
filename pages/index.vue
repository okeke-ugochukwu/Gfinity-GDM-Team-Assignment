<template>
  <div class="base">
    
    <headerBar />

    <!-- main content -->
    <main>
      <titleBar/>

      <section class="player-list">
        
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
          this.players = players
        })
    }
  
  }
</script>


