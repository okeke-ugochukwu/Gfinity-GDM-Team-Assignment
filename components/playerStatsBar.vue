<template>
    <NuxtLink :to="player.name.toLowerCase().replace(/\s/g, '-')">
        <div class="player-stats-bar">
            <div class="centered_inner">
                <div>
                    {{player.name.toUpperCase()}} 
                </div>
                
                <div>
                    <ul>
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
                ]
                  }
            }
        }
</script>

