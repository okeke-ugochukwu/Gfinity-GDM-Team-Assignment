<template>
    <div class="player-bar">
        <div class="centered_inner">
            <div>
                LIONEL MESSI 
            </div>
            
            <div>
                <ul>
                    <li v-for="item in this.titleBarItems">
                        {{item}}
                    </li>
                </ul>
            </div>
            
        </div>
    </div>
</template>

<script>
    export default {
        name: 'playerBar',

        data() {
            return {
                titleBarItems: [
                     '95', 'RW', 'RW', '85', '92', '91', '95', '34', '65', 'ML'   
                ]
                  }
            }
    }
</script>

