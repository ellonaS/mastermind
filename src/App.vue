<template>
  <div id="app">
    <game-header/>
    <router-view id="routerView"/>
  </div>
</template>

<script>
import GameHeader from "@/components/GameHeader.vue";

export default {
  components: {
    GameHeader
  }
  
}
</script>
<style>
#routerView {
  margin-top: 5%;
  margin-left: 5%;
  margin-right: 5%;
}
</style>
