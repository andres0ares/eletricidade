<template>
  <v-container>
    <h1>Eletricidade</h1>
    <ConvertMulti class="ma-2"/>
    <RlcEmSerie class="ma-2"/>
    <RlcEmParalelo class="ma-2"/>
  </v-container>
</template>

<script>
import ConvertMulti from './ConvertMulti.vue';
import RlcEmSerie from './RlcEmSerie.vue';
import RlcEmParalelo from './RlcEmParalelo';

export default {
  name: 'HomeMain',
  components: {
    ConvertMulti,
    RlcEmSerie,
    RlcEmParalelo,
  },
  data: () => ({
   lar: "home",
  }),
}
</script>
