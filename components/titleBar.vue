<template>

   <!-- TITLE BAR -->
    <div class="text-white font-normal pb-[9.13px] pt-[34px] bg-black lg:pt-[57px]">

      <!-- CENTERED INNER -->
      <div class="w-[77%] m-auto flex justify-between">

         <!-- NAME TITLE -->
         <div class="flex items-center w-[20%]">
            Name
            
            <!-- controls -->
            <div class="flex flex-col ml-[4px] text-xs">
               <button>
                  <img src="@/assets/imgs/up-arrow.svg" alt="up" />
               </button>
               
               <button>
                  <img src="@/assets/imgs/down-arrow.svg" alt="down" />
               </button>
            </div>
         </div>
         
         <!-- RATING TITLES -->
         <div class="flex w-max">
            <ul class="flex content-between">
               <li 
                  class="
                     flex items-center h-7 text-xs [&:not(:first-child)]:px-[14px] 
                     first:pr-[14px] border-r border-r-[#606060]
                  "
                  v-for="item in this.titleBarItems" :key="item"
               >

                     {{item}}

                     <!-- CONTROLS -->
                     <div class="flex flex-col ml-[4px] text-xs">
                        <button>
                           <img src="@/assets/imgs/up-arrow.svg" alt="up" />
                        </button>
                        
                        <button>
                           <img src="@/assets/imgs/down-arrow.svg" alt="down" />
                        </button>
                     </div>
               </li>
            </ul>
         </div>

      </div>

    </div>

</template>

<script>
   import atrrTitleItems from "../data/attributes"

    export default {
      name: "titleBar",

      data() {
         return {
               titleBarItems: atrrTitleItems
            }
         }
      }
</script>

