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
  const sanityClient = require('@sanity/client')
  const client = sanityClient({
    projectId: '21fy9g0s',
    dataset: 'production',
    apiVersion: '2021-03-25',
    useCdn: true,
  })
  const query = '*[_type == "fifaCard"]'

  
  

  export default {
    name: 'IndexPage',

    data() {
      return {
        players: []
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


