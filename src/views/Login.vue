<template>
  <v-container class="cintelinkBg content" grid-list-md text-center fluid>
      <LoginBox/>
  </v-container>

</template>

<script>
import LoginBox from '../components/LoginBox.vue';
export default {
  components: {
    LoginBox
  },
  name: 'Login',
  data: () => ({
    //
  }),
};
</script>
<style>
.cintelinkBg {
  background-image: url('../assets/cintelink-bg.jpg');
  height: 100vh;
  background-size: cover;
}

.content {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
