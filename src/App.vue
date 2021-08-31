<template>
  <div id="app">
   <navbar/>
   <userform/>
  </div>
</template>

<script>
import navbar from './components/navbar.vue'
import userform from './components/form.vue'

export default {
  name: 'App',
  components: {
    navbar,
    userform,
  }
}
</script>

<style>
#app {
  background-color: rgba(211, 229, 241, 0.863);
}
</style>
