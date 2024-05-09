<template>
  <main>  
    <NotificationList />
  </main>
</template>

<script setup>
import NotificationList from './components/NotificationList.vue';
</script>

<style scoped>
main {
  padding: 1rem 0;
}

@media screen and (min-width:1024px) {
  main {
    width: 50rem;
  }
}
</style>
