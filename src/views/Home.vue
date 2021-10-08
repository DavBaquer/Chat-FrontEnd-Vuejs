<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HomeChat msg="CHAT PERSISTENTE"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeChat from '@/components/HomeChat.vue'

export default {
  name: 'Home',
  components: {
    HomeChat
  }
}
</script>
