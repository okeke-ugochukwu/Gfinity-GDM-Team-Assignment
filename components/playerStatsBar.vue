<template>
    <NuxtLink :to="player.slug.current">

      <!-- PLAYER STATS BAR -->
      <div 
         class="
            text-white font-normal py-[12px] 
            border-b border-black bg-rs-grey2 
            hover:scale-[1.03] hover:border hover:bg-[#44c99430]
         "
      >

         <!-- CENTERED INNER -->
         <div class="w-[77%] m-auto flex justify-between">

               <!-- PLAYER NAME -->
               <div class="flex items-center text-[10px] w-1/5 font-bold">
                  {{player.name.toUpperCase()}} 
               </div>
               
               <!-- PLAYER ATTRIBUTES -->
               <div class="flex justify-between w-max text-xs">
                  <ul class="flex">
                     <li>
                           {{player.rating}}
                     </li>

                     <li>
                           {{player.position}}
                     </li>

                     <li>
                           {{player.position}}
                     </li>

                     <li>
                           {{player.statistics.pace.average}}
                     </li>

                     <li>
                           {{player.statistics.shooting.average}}
                     </li>

                     <li>
                           {{player.statistics.passing.average}}
                     </li>

                     <li>
                           {{player.statistics.dribbling.average}}
                     </li> 

                     <li>
                           {{player.statistics.defense.average}}
                     </li>

                     <li>
                           {{player.statistics.physical.average}}
                     </li>

                     <li>
                           {{player.workRatesAttacking.charAt(0)}}/{{player.workRatesDefensive.charAt(0)}}
                     </li>

                  </ul>
               </div>        
         </div>
      </div>

    </NuxtLink>
</template>

<script>
    export default {
        name: 'playerBar',
        
        props: {
            player: {
                type: Object,
                default: () => {}
            },
        },

        data() {
         return {
               titleBarItems: [
                  '95', 'RW', 'RW', '85', '92', '91', '95', '34', '65', 'ML'   
               ],

            //    playerAttributs: [
            //       this.player.rating,
            //       this.player.position,
            //       this.player.poistion,
            //       this.player.statistics.pace.average,
            //       this.player.statistics.shooting.average,
            //       this.player.statistics.passing.average,
            //       this.player.statistics.dribbling.average,
            //       this.player.statistics.defense.average,
            //       this.player.statistics.physical.average,
            //       this.player.workRatesAttacking.charAt(0)/player.workRatesDefensive.charAt(0)
            //    ]
            }
         }
            
        }
</script>

<style lang="scss" scoped>
  ul {
   li {
      @apply
      flex items-center justify-center h-7 text-xs font-bold rounded 
      mr-[7px] ml-[11px] w-[46px] py-[2] [&:not(:first-child)]:px-[14px]
      first:bg-white text-black;


      &:not(:first-child) {
         @apply px-[14px]
      }
      

      &:first-child {
         @apply bg-white text-black;
      }

      &:nth-child(2), 
      &:nth-child(3),
      &:nth-child(10) {
         @apply bg-black text-white;
      }

      &:nth-child(4),
      &:nth-child(5),
      &:nth-child(6),
      &:nth-child(7),
      &:nth-child(8),
      &:nth-child(9) {
         @apply 
         bg-black text-white
         border border-white
         rounded
      }
   }

  }
</style>

