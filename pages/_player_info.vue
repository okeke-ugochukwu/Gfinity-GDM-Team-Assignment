<template>
   <!-- BASE -->
   <div class="w-full min-w-[375px] min-h-screen bg-[#44444B] py-[0.05px]">
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
      
      <main v-else class="max-w-[1024px] min-h-screen m-auto pt-[66px] bg-black " >

         <div class="w-[91.73%] m-auto lg:px-[23px] lg:w-full">
            <!-- PLAYER ATTR BOARD -->
            <section class="
               attributes-board  mt-[19px] rounded-[12.66px] p-3 mb-[43px] 
               lg:flex gap-[54px] lg:pb-[81px] lg:mt-[66px] xl:w-full" 
               > 
               <!-- IMAGE -->
               <div class="
                  min-w-[182px] w-1/2 m-auto lg:w-max-[182px] mb-[20px] 
                  lg:mb-0 lg:m-0 lg:   max-w-[182px]"
               >
                  <img 
                     :src="urlFor(playerInView[0].cardImage)" :alt="playerInView[0].name.toLowerCase().replace(/\s/g, '-') + '-card'"
                     class="w-full"
                  >
               </div>

               <!-- ATTRIBUTES -->
               <div class="attributes_list grid grid-cols-3 gap-x-3 gap-y-[25px]
                     lg:grid-cols-6"
                  >
                  <ul
                     v-for="attribute in Object.entries( retouchedStats(playerInView[0].statistics) )" :key="attribute"
                     class="inline-block text-white"
                  >
                     <li class="
                        flex justify-between items-center px-[0]
                        font-bold text-sm border-y-2 border-solid border-white py-[6px]    
                        lg:min-w-[102px]"
                     >
                        {{ attribute[0].slice(0, 3).toUpperCase() }}
                     </li>

                     <li 
                        v-for="listItem in Object.entries(retouchedObject(attribute[1]))" :key="listItem" 
                        class="flex justify-between items-center py-[12.5px] px-[0] lg:min-w-[102px]
                        [&:nth-child(2)]:pt-[16px]  "
                     >
                        <span class="inline-block font-bold text-[10px]">{{ listItem[0].split(/(?=[A-Z])/).join(' ').replace(/(^\w|\s\w)/g, m => m.toUpperCase()) }}</span>
                        <span class="inline-block font-bold text-sm"> {{ listItem[1] }} </span>
                     </li>
                  </ul>
               </div>
            </section>
  

            <!-- PLAYER SUMMARY -->
            <section class="text-white lg:pl-[33px]">

               <!-- PLAYER NAME -->
               <div class="flex items-end lg:mb-[45px]">
                  <h1 class="text-3xl font-bold mr-2.5">
                     {{ playerInView[0].name }}
                  </h1>

                  <nuxt-link 
                     to="/" 
                     class="inline-block text-[#848282] pb-[3px]
                     text-xs border-b-[0.5px] border-dashed"
                  >
                     View all cards
                  </nuxt-link>
               </div>

               <!-- PLAYER DETAILS -->
               <div class="">
                  <ul 
                     class="lg:flex"
                  >

                     <li 
                        v-for="listItem in Object.entries(playerCompiledSummary(playerInView[0]))" :key="listItem" 
                        class="flex justify-between text-sm py-[17px] border-b-2 border-solid border-[#44444B]
                        lg:flex-col lg:border-b-0 lg:[&:not(:last-child)]:border-r-2 
                        lg:[&:not(:first-child)]:px-4 lg:[&:not(:first-child)]:pr-4 lg:py-[5px] lg:gap-[18px] lg:min-w-[117px]"
                     >    
                        <span class="lg:text-[#848282]">{{ listItem[0].split(/(?=[A-Z])/).join(' ').replace(/(^\w|\s\w)/g, m => m.toUpperCase()) }}</span>
                        <span> {{ listItem[1] }} </span>
                     </li>
                     
                  </ul>
               </div>
            </section>
         </div>

         <footerBar />
      </main>
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
               console.log(playerInView)                
            })
      },


      methods: {

          urlFor(imgSrc) {
            return builder.image(imgSrc)
         },

         retouchedObject(atrrObject) {
            //remove 'average' property and return object for iteration
            delete atrrObject.average;
            return atrrObject
         },

         retouchedStats(statsObject) {
            //rearrage the players statsobject before iteration
            const retouchedStats = {
               'pace': statsObject.pace,
               'shooting': statsObject.shooting,
               'passing': statsObject.passing,
               'dribbling': statsObject.dribbling,
               'defense': statsObject.defense,
               'physical': statsObject.physical
            }

            return retouchedStats;
         },

         playerCompiledSummary(playerInView) {
            //get property needed for iteration
            const playerSummary = {
               'club': playerInView.club,
               'league': playerInView.league,
               'nation': playerInView.nation,
               'strongFoot': playerInView.strongFoot.replace(/(^\w|\s\w)/g, m => m.toUpperCase()),
               //check if value is a regex or regular string before retuning manipulated value
               'age': playerInView.age.slice(playerInView.age.lastIndexOf(' ') + 1) === "old"? playerInView.age.split(/\s+/).slice(0, 1).join(" ") : "N\\A",  
               'height': playerInView.height,
               'workrates': playerInView.workRatesAttacking + ' ' + '/' + ' ' + playerInView.workRatesDefensive
            }

            return playerSummary;
         }
      }
   }
</script>

<style lang="scss" scoped>
   .attributes-board {
      background: linear-gradient(180deg, #0F0F0F 0%, #161616 52.33%, #0D0D0D 100%);
   }
</style>


