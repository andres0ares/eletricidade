<template>
  <v-container>
    <h1>Eletricidade</h1>
    <ConvertMulti class="ma-2"/>
    <SigmaCl class="ma-2"/>
  </v-container>
</template>

<script>
import ConvertMulti from './ConvertMulti.vue';
import SigmaCl from './SigmaCl.vue';

export default {
  name: 'HomeMain',
  components: {
    ConvertMulti,
    SigmaCl,
  },
  data: () => ({
   lar: "home",
  }),
}
</script>
