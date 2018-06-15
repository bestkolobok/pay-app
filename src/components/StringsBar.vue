<template>
    <div class="conteiner">
        <v-container class="strings" grid-list-md text-xs-center>
            <v-layout row wrap v-for="(item, index) in base" :key="index">
                <v-flex xs1>
                    <p class="strings__bullet">String {{index+1}} </p>
                </v-flex>
                <v-flex xs10 justify-start>
                    <p class="strings__string text-xs-left">{{item.string}}</p>
                </v-flex>
                <v-flex xs1>
                    
                </v-flex>
            </v-layout>
        </v-container>
    </div>
</template>

<script>
import {HTTP} from '@/common/http.js'

export default {
    name: 'StringsBar',
    data () {
        return {
            base: [
                {string: 'ajhgvnnuodfuojgepkghfucubvcvbng', oldString: ''},
                {string: 'jmohgduhvbndhgtseiropsokmbeqfnf', oldString: ''},
                {string: 'dngbdbvzbvdhyuvd', oldString: ''},
                {string: 'iypyuoybnqtydbhcchyfkgk', oldString: ''}
            ]
        }
    },
    methods: {
        satrtSort(){

        },
        revertSort(){

        },
        randomSort(){

        }
    },
    mounted(){
        this.$eventHub.$emit('start-sort', this.satrtSort())
        this.$eventHub.$emit('revert-sort', this.revertSort())
        this.$eventHub.$emit('random-sort', this.randomSort())
    } 
}
</script>

<style lang="scss" scoped>
    .conteiner{
        margin-top: 30px;
        height: 60vh;
        .strings{
            &__bullet{
                color: red;
            }
            &__string{
                margin-left: 20px;
            }
        }
    }
</style>