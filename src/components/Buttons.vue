<template>
  <div class="conteiner text-xs-center">
    <v-container grid-list-md>
        <v-layout row wrap justify-center>
            <v-flex class="offset-1 text-xs-center" xs2>
                <v-btn color="accent" block @click.native="start">SORT</v-btn>
            </v-flex>
            <v-flex class="offset-1 text-xs-center" xs2>
                <v-btn color="accent" block @click.native="revert">REVERT</v-btn>
            </v-flex>
            <v-flex class="offset-1 text-xs-center" xs2>
                <v-btn color="accent" block @click.native="random">RANDOM</v-btn>
            </v-flex>
            <v-flex class="offset-1 text-xs-center" xs2>
                <v-btn
                    :loading="pushing"
                    :disabled="pushing"
                    color="secondary"
                    block
                    @click.native="pushServer"
                >
                    Push to serv
                    <span slot="pushing" class="custom-loader">
                        <v-icon light>cached</v-icon>
                    </span>
                </v-btn>
            </v-flex>
            <v-flex class="offset-1 text-xs-center" xs2>
                <v-btn
                    :loading="geting"
                    :disabled="geting"
                    color="secondary"
                    block
                    @click.native="getServer"
                >
                    Get from serv
                    <span slot="geting" class="custom-loader">
                        <v-icon light>cached</v-icon>
                    </span>
                </v-btn>
            </v-flex>
        </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
    name: 'Buttons',
    data () {
        return {
            pushing: false, 
            geting: false
        }
    },
    methods: {
        start(){
            this.$eventHub.$emit('start-sort')
        },
        revert(){
            this.$eventHub.$emit('revert-sort')
        },
        random(){
            this.$eventHub.$emit('random-sort')
        },
        pushServer(){
            this.pushing = true
            firebase.database().ref('data/first_data').set({
               base: this.$eventHub.base
            })
            .then(() => this.pushing = false)
            .catch(error => console.log (error))
        },
        getServer(){
            this.geting = true
            firebase.database().ref('/data/first_data').once('value')
            .then(data => {
                this.$eventHub.base = data.val().base
                this.$eventHub.$emit('server-get')
                this.geting = false
            })
            .catch(error => console.log (error))
        }   
    }
}
</script>

<style lang="scss" scoped>
   .custom-loader {
    animation: loader 1s infinite;
    display: flex;
  }
  @keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>