<template>
  <div id="app">
    <h1> {{ title }} </h1>
    <appTextArea @userMessageUpdated='logMessage'></appTextArea>
  </div>
</template>

<script>
import TextArea from './components/TextArea.vue';
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
      title: 'Synonomizer',
      posts: ''
    }
  },
  methods: {
    logMessage(wordArray) {
      console.log(wordArray);
      for(var i = 0; i < wordArray.length; i++){
        axios.get("https://api.datamuse.com/words?rel_syn=" + wordArray[i])
        .then(response => {
        this.words = response.data
        console.log(this.words);
        })
      } 
    }
  },
  components: {
    appTextArea: TextArea
  }
  // created() {
  //   axios.get("https://api.datamuse.com/words?rel_syn=fear")
  //     .then(response => {
  //     this.posts = response.data
  //   })
  //   .catch(e => {
  //     this.errors.push(e)
  //   })
  // }
}
</script>

<style>
#app {
  text-align: center;
}
h1 {
  font-size: 30px;
  margin: 20px 0px;
}
button {
  margin: 20px 0px 0px 0px;
}
</style>
