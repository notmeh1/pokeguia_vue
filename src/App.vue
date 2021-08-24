<template>
 <div id="app">
   <DarkMode/>
 </div>
</template>

<script>
import DarkMode from './components/DarkMode'

export default {
  name: 'App',
  components: {
    DarkMode,
  }
}
</script>

<style>
body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}
</style>
