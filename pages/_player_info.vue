<template>
  <div class="w-full min-w-max h-max bg-rs-grey">

    
    <headerBar />

    
    <main class="w-full min-h-screen m-auto pt-[66px] bg-black">

      <!-- PLAYER ATTR BOARD -->
      <section class="bg-rs-grey w-[91.73%] m-auto mt-[19px] rounded-[12.66px] p-3">
         <div v-if="$fetchState.pending">Fetching player</div>
         <div v-else-if="$fetchState.error">Something went wrong</div>
         
         <!-- PLAYER IMAGE + ATTRIBUTES -->
         <div  v-else class="w-full">

            <!-- IMAGE -->
            <div class="w-full mb-[20px]">
               <img 
                  :src="urlFor(playerInView[0].cardImage)" :alt="playerInView[0].name.toLowerCase().replace(/\s/g, '-') + '-card'"
                  class="w-[182px] m-auto"
               >
            </div>

            <!-- ATTRIBUTES -->
               <div class="attributes_list grid grid-cols-3 gap-x-3 gap-y-[25px]">
                  <ul v-for="attribute in Object.entries( retouchedStats(playerInView[0].statistics) )" :key="attribute">
                     <li>
                        {{ attribute[0].slice(0, 3).toUpperCase(  ) }}
                     </li>

                     <li v-for="listItem in Object.entries(retouchedObject(attribute[1]))" :key="listItem">
                        <span>{{ listItem[0].split(/(?=[A-Z])/).join(' ').replace(/(^\w|\s\w)/g, m => m.toUpperCase()) }}</span>
                        <span> {{ listItem[1] }} </span>
                     </li>
                  </ul>

                  
               </div>
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
import { setTimeout } from 'timers'
  const builder = imageUrlBuilder(client)


   export default {
      name: 'PlayerDetailsPage',
      
      data() {
         return {
            playerInView: {},
            playerAttributes: {}
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
               
               console.log(playerInView.statistics)
                   
            })
      },


      methods: {

          urlFor(imgSrc) {
            return builder.image(imgSrc)
         },

         retouchedObject(atrrObject) {
            delete atrrObject.average;
            return atrrObject
         },

         retouchedStats(statsObject) {
            const retouchedStats = {
               'pace': statsObject.pace,
               'shooting': statsObject.shooting,
               'passing': statsObject.passing,
               'dribbling': statsObject.dribbling,
               'defense': statsObject.defense,
               'physical': statsObject.physical
            }

            return retouchedStats;
         }
      },

      updated() {
         console.log('updated');
      },

   }
</script>

<style lang="scss" scoped>
   .attributes_list {
      ul {
         display: inline-block;
         width: 102px;
         min-width: 102px;
         color: white;

         li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12.5px 0px;

            //ATTRIBUTE HEADINGS
            &:nth-child(1) {
               font-weight: 700;
               font-size: 0.875rem; //14px
               border-top: 2px solid white;
               border-bottom: 2px solid white;
               padding: 6px 0px;
            }

            &:nth-child(2) {
               padding-top: 16px;
            }

            span {
               display: inline-block;
               font-weight: 700;

               &:nth-child(1) {
                  font-size: 0.625rem; //10px
               }

               &:nth-child(2) {
                  font-size: 0.875rem; //14px
               }
            }
         }
      }
   }
</style>


