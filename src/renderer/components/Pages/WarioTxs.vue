<template>
    <transition name="fade">
            <div class="wario_seq" v-if="show_wario">
                <div class="wario_standing_animated">
                    <div class="wario_standing">

                    </div>

                    <div v-if="usd < 1">
                        <div class="bubble" :style="`background-image: url(${this.path_bubble(0)})`"></div>
                    </div>

                    <div v-else-if="usd < 100">
                        <div class="bubble" :style="`background-image: url(${this.path_bubble(1)})`"></div>
                    </div>

                    <div v-else-if="usd < 500">
                        <div class="bubble" :style="`background-image: url(${this.path_bubble(2)})`"></div>
                    </div>

                    <div v-else-if="usd < 1500">
                        <div class="bubble" :style="`background-image: url(${this.path_bubble(3)})`"></div>
                    </div>

                    <div v-else-if="usd >= 1500">
                        <div class="bubble" :style="`background-image: url(${this.path_bubble(4)})`"></div>
                    </div>
                </div>

                <div class="grass_container">
                    <div class="grass"></div>
                    <div class="grassfill"></div>
                </div>
            </div>
    </transition>

</template>

<script>
    export default {
        name: "WarioTxs",
        computed: {
            wallet() {
                return this.$store.getters.wallet;
            },
            usd(){
                return (this.$store.getters.usd_rate / 1000) * this.$store.getters.wallet.balance;
            },
            bubble_img() {
                let rate = this.$store.getters.usd_rate;
                let usd = (rate / 1000) * this.$store.getters.wallet.balance;

                if(usd < 1){
                    return this.path_bubble(0);
                } else if(usd < 100){
                    return this.path_bubble(1);
                } else if(usd < 500){
                    return this.path_bubble(2);
                } else if(usd < 1000){
                    return this.path_bubble(3);
                } else if(usd < 1000){
                    return this.path_bubble(4);
                }
            }
        },
        data () {
            return {
                'show_wario': true
            }
        },
        methods: {
            path_bubble(number) {
                // vuejs+webpack sux
                return require(`../../assets/bubbles/${number}.png`);
            }
        },
        mounted() {
            setTimeout((event) => {
                this.show_wario = false;
            }, 4000);
        }
    }
</script>

<style scoped>

</style>