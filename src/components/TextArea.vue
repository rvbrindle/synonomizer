<template>
    <div>
        <textarea name='user-input' placeholder="Type here..." v-model='userInput'></textarea>
        <button class='submit' type='submit' value='submit' @click='findIndexes'> SYNONOMIZE! </button>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                userInput: ''
            }
        },
        methods: {
                       
            findIndexes () {
                var indicies = {
                        openIndicies: [],
                        closeIndicies:  []
                };
                for (var i = 0; i < this.userInput.length; i++){
                    if(this.userInput[i] === '['){
                        indicies.openIndicies.push(i +1);
                    }
                    else if(this.userInput[i] === ']'){
                        indicies.closeIndicies.push(i);
                    }
                }
                this.collectWords(indicies);
            },

            collectWords(indicies) {
                var userWords = [];
                for (var i = 0; i < 10; i++){
                    var difference = Math.abs(indicies.openIndicies[i] - indicies.closeIndicies[i]); 
                    var word = this.userInput.substr(indicies.openIndicies[i], difference);
                    if (word == '') {
                        break;
                    }
                    userWords.push(word);
                }
                this.returnUserWord(userWords);
            },

            returnUserWord(userWords) {
                this.$emit('userMessageUpdated', userWords);
                // this.userInput = '';
            }
        }
    }
</script>

<style>
textarea {
   background-color: #999;
   width: 80%;
   min-height: 300px;
   display: block;
   margin: 0 auto;
   color: white;
   font-size: 20px;
}
</style>