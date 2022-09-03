<template>
  <div class="base">
    
    <headerBar />

    <!-- main content -->
    <main>

      <section class="player-cBoard">
        <div class="player-cBoard_img">

        </div>

        <div class="player-cBoard_attr">

        </div>

        <div class="player-cBoard_attr2">
          
        </div>
      </section>

      <section class="player-summary">
          <div class="palyer-summary_titl">
            {{players}}
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

  export default {
    name: 'PlayerDetailsPage',
    
    data() {
      return {
        player: [],
        players: {}
      }
    },

    async asyncData({ params }) {
      await client.fetch(query)
      .then ((players) => {
        const player = players.filter(player => player.slug.current = params)
        return players
      })
    }

  }
</script>


