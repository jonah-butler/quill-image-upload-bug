<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <Quill />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from '@/components/HelloWorld.vue';
import Quill from '@/components/Quill.vue';

export default defineComponent({
  name: 'Home',
  components: {
    HelloWorld,
    Quill
  },
});
</script>
