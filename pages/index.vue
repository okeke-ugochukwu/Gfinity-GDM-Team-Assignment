<template>
  <div class="base">
    
    <headerBar />

    <!-- main content -->
    <main>
      <titleBar/>

      <section class="player-list">
        <playerBar />
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

  client.fetch(query).then ((cards) => {
    console.log(cards)
  })
  

  export default {
    name: 'IndexPage',

    data() {
      return {
        players: []
      }
    },
  
  }
</script>


