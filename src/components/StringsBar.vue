<template>
    <div class="conteiner">
        <v-container class="strings" grid-list-md text-xs-center>
            <v-layout row wrap v-for="(item, index) in base" :key="index">
                <v-flex xs1 align-center d-flex>
                    <span class="strings__bullet">String {{index+1}} </span>
                </v-flex>
                <v-flex xs7 justify-start align-center d-flex>
                    <span class="strings__string text-xs-left">{{item.string}}</span>
                </v-flex>
                <v-flex xs1 align-center d-flex>
                    <span>length {{item.length}}</span>
                </v-flex>
                <v-flex xs1 align-center d-flex>
                    <span>vow {{item.vowels}}</span>
                </v-flex>
                <v-flex xs1 align-center d-flex>
                    <span>cons {{item.consonants}}</span>
                </v-flex>
                <v-flex xs1>
                    <v-btn flat icon color="primary">
                        <v-icon>close</v-icon>
                    </v-btn>
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
            alphabet: {
                vowels: ['a', 'e', 'i', 'o', 'u', 'y'],
                consonants: ['b', 'c', 'd', 'f', 'g', 'h', 'j', 'k', 'l', 'm', 'n', 'p', 'q', 'r', 's', 't', 'v', 'w', 'x', 'z']
            },
            base: [
                {string: 'ajhutrvmmfhmgmfghmhoiow', oldString:'', length:'', vowels:'', consonants:''},
                {string: 'jmohgduhvbndhgtseiropsokmbeqfnf', oldString: '', length:'', vowels:'', consonants:''},
                {string: 'baaaaabbbbbaaaaba', oldString:'', length:'', vowels:'', consonants:''},
                {string: 'iypyuoybnqtydbhcchyfkgk', oldString:'', length:'', vowels:'', consonants:''}
            ]
        }
    },
    methods: {
        revertStateSet(){
            this.base.forEach(data => {
                data.oldString = data.string
            })
        },
        calcState(){
            this.base.forEach(data => {
                data.length = data.string.length
                data.vowels = 0
                data.consonants = 0
                const stringArr = data.string.split('')
                stringArr.forEach(char => {
                    if(this.alphabet.vowels.includes(char)){
                        data.vowels ++
                    }else{
                        data.consonants ++
                    }
                })
            })
        },
        satrtSort(){
            let endVowel = []
            this.base.forEach(data => {
                // data.oldString = data.string
                let stringArr = data.string.split('')
                let sortStringArr = []
                if(endVowel.length > 0 ){endVowel.forEach(vowel => {stringArr.unshift(vowel)})}
                let oldLetter = null
                // stringArr.forEach((letter, index, arr) => {
                //     if(
                //         index === 0 || 
                //         this.alphabet.vowels.includes(letter) || 
                //         (!this.alphabet.vowels.includes(letter) && this.alphabet.vowels.includes(oldLetter)) ||
                //         (this.alphabet.vowels.includes(letter) && !this.alphabet.vowels.includes(oldLetter) && oldLetter !== null)
                //     ){
                //         sortStringArr.push(letter)
                //     }else{
                //         arr.push(letter)
                //         // console.log(stringArr)
                //     }
                //     oldLetter = letter
                // })


                for(let i = 0, state = true; state; i += 1) {
                    const letter = stringArr[i]
                    if(
                        i === 0 || 
                        // this.alphabet.vowels.includes(letter) || 
                        (!this.alphabet.vowels.includes(letter) && this.alphabet.vowels.includes(oldLetter)) || 
                        (this.alphabet.vowels.includes(letter) && !this.alphabet.vowels.includes(oldLetter) && oldLetter !== null)
                    ){
                        sortStringArr.push(letter)
                    }else{
                        const remain = stringArr.slice(i)
                        if(remain.length > 0){
                            let vowels = true, consonants = true
                            remain.forEach((char, index) =>{
                                if(this.alphabet.vowels.includes(char)){
                                    consonants = false
                                }else{
                                    vowels = false
                                }
                            })
                            if((vowels && !consonants) || (!vowels && consonants)) {
                                sortStringArr.push(letter)
                            }else{
                                stringArr.push(letter)
                            }
                        }
                    }
                    oldLetter = letter
                    if(i === stringArr.length - 1 || i === 1000){state = false}
                }
                endVowel = []
                while(this.alphabet.vowels.includes(sortStringArr[sortStringArr.length-1])){
                    endVowel.push(sortStringArr.pop())
                }
                // endVowel = this.alphabet.vowels.includes(sortStringArr[sortStringArr.length-1]) ? sortStringArr.pop() : null
                data.string = sortStringArr.join('')
            })
            this.calcState()
        },
        revertSort(){
            this.base.forEach(data => {
                data.string = data.oldString
            })
            this.calcState()
        },
        randomSort(){
            this.base.forEach(data => {
                const length = data.string.length
                let randomString = ''
                for(let i=0; i<length; i++){
                    const randomCode = Math.floor(Math.random() * 26) + 97
                    randomString += String.fromCharCode(randomCode)
                }
                data.string = randomString
                // 97 122
            })
            this.calcState()
        }
    },
    mounted(){
        this.revertStateSet()
        this.calcState()
        this.$eventHub.$on('start-sort', this.satrtSort)
        this.$eventHub.$on('revert-sort', this.revertSort)
        this.$eventHub.$on('random-sort', this.randomSort)
    } 
}
</script>

<style lang="scss" scoped>
    .conteiner{
        margin-top: 30px;
        height: 60vh;
        .strings{
            &__bullet{
                color: #d54747;
            }
            &__string{
                margin-left: 20px;
            }
        }
    }
</style>