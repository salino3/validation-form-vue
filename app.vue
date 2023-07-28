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
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 18px;

    padding: 20px 10px;   
    color: blue;
}
</style>