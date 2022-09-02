<template>
    <div class="title-bar">
        <div class="centered_inner">
            <div>
                Name
                
                <!-- controls -->
                <div class="title-bar__controls">
                    <button>
                        <img src="@/assets/imgs/up-arrow.svg" alt="up"></img>
                    </button>
                    
                    <button>
                        <img src="@/assets/imgs/down-arrow.svg" alt="down"></img>
                    </button>
                </div>
            </div>
            
            <div>
                <ul>
                    <li v-for="item in this.titleBarItems">

                        {{item}}

                        <div class="title-bar__controls">
                            <button>
                                <img src="@/assets/imgs/up-arrow.svg" alt="up"></img>
                            </button>
                            
                            <button>
                                <img src="@/assets/imgs/down-arrow.svg" alt="down"></img>
                            </button>
                        </div>
                    </li>
                </ul>
            </div>
            
        </div>
    </div>
</template>

<script>
    export default {
        name: "titleBar",

        data() {
            return {
                titleBarItems: [
                    'OVR', 'POS', 'Type', 'PAC', 'SHO', 'PAS', 'DRI', 'DEF', 'PHY', 'WR'   
                ]
                  }
            }
           
    }
</script>

