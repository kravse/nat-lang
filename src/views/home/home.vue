<template>
  <div>
    <h1>Home</h1>
    <p>{{sampleItem}}</p>
    <router-link :to="{name: 'about'}">About Page</router-link>
  </div>
</template>

<script>
import Vue from 'vue';

export default Vue.extend({
  name: 'Home',
  data() {
    return {
      sampleItem: ''
    }
  },
  created: function () {
    this.sampleItem = 'hello world'
  },
  // components: {
  // },
  // computed: {},
  // mounted: function () {

  // },
  // methods: {
  //   myMethod: function () {

  //   }
  // },
  // watch:{
  //   thing (to, from){
  //   }
  // }

});
</script>
<style scoped src="./home.styl" lang="stylus"></style>
