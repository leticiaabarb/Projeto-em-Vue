<template>
  <div class="main">
    <h1>This is an register page</h1>
    <RegisterObjects/>
  </div>
</template>


<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import RegisterObjects from '@/components/RegisterObjects.vue'; // @ is an alias to /src

@Options({
  components: {
    RegisterObjects,
  },
})
export default class RegisterView extends Vue {}
</script>
