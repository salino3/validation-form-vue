<template>
  <main class="default">
   <Header />
     <div class="pages">
       <NuxtPage />
      </div>
  </main>
</template>

<script>
import Header from '@/components/Header';

export default {
  components: {
    Header
  }
}
</script>

<style>

.pages {
    padding: 20px 10px;   
    color: blue;
}
</style>