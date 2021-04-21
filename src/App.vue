<template>
  <div id="app">
    <div class="app-inner">
      <router-view/>
      <site-footer/>
    </div>
  </div>
</template>
<script>
import Vue from 'vue';
import footer from '@/components/footer/footer.vue'

export default Vue.extend({
  name: 'App',
  components: {
    'site-footer': footer,
  },
  computed: {
    overlay: function () {
      return this.$route.name !== 'home'
    }
  }
});
</script>
<style src="@/assets/styles/main.styl" lang="stylus"></style>

