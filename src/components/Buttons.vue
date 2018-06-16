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
                <v-btn color="accent" block @click.native="pushServer">Push to serv</v-btn>
            </v-flex>
            <v-flex class="offset-1 text-xs-center" xs2>
                <v-btn color="accent" block @click.native="getServer">Get from serv</v-btn>
            </v-flex>
        </v-layout>
    </v-container>
  </div>
</template>

<script>
import {HTTP} from '@/common/http.js'
export default {
    name: 'Buttons',
    data () {
        return {
            
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

        },
        getServer(){

        }
           
    }, 
    mounted(){
        
    }
}
</script>

<style lang="scss" scoped>
   
</style>