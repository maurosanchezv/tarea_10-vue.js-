<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- Código 1. HelloWorldコンポーネントを使用 -->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// Código 2. HelloWorldコンポーネントをimport
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  // Código 3. コンポーネントを登録
  components: {
    HelloWorld
  }
}
</script>