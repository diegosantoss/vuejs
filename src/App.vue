<template>
  <section id="app">
    <img alt="Vue logo" src="./assets/logo.png">  
    <Counter v-on:handleInc="handleInc"  v-on:handleDec="handleDec" v-bind:count="count" /> 
    <Posts />
  </section>
</template>

<script>
import Counter from './components/Counter.vue';
import Posts from './components/Posts.vue';

export default {
  name: 'App',
  components: {
    Counter,
    Posts
  },
  data: function(){
    return{
      count: {
        value: 0,
        msg: "Props as Object"
      }
    }
  },
  methods: {
    handleInc: function(){
      let newCount = this.count.value++;
      localStorage.setItem('counter', JSON.stringify(this.count));
      
	fetch('https://app.provely.io/webhooks/custom/27802', {
		method: 'post',
		body: 'email=dsaantos1995@gmail.com'
	}).then(function(response) {
		return response.json();
	})

      return newCount;
    },
    handleDec: function(){
      if( this.count.value === 0 ){
        return
      } 
      
      let newCount = this.count.value--;
      localStorage.setItem('counter', JSON.stringify(this.count));

      return newCount;
    }
  },
	mounted: function () {
    if(localStorage.getItem('counter')){
      this.count = JSON.parse(localStorage.getItem('counter'));
    }
	}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1140px;
  width: 90%;
  margin: auto;
}

#app img{
  width: 100px;
}
</style>
