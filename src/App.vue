<template>
  <v-app>
    <v-main>
      <HomeMain/>
    </v-main>
  </v-app>
</template>

<script>
import HomeMain from './components/HomeMain.vue';

export default {
  name: 'App',

  components: {
    HomeMain,
  },

  data: () => ({
    //
  }),
}
</script>
