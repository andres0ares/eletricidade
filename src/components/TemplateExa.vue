<template>
<div>

    <v-card
    class="mx-auto color-wt"
    :color="color"
    max-width="400"
    v-if="open"

    >
    <v-card-title>
      <span class="text-h6 font-weight-light">{{ name }}</span>
    </v-card-title>
    
    <v-container v-for="(valor, idx) in input" v-bind:key="idx">
        <v-row>
            <v-col sm="3"><p>{{ valor.n }}</p></v-col>
            <v-col sm="9">
                <input class="input-cl" type="number" :name="valor.n" :id="`${valor.n}_id`" 
                @change="(evt) => valor.v = evt.target.value">
            </v-col>
        </v-row>
    </v-container>
        
    <v-container class="result ma-2" v-for="(res, idx) in calculo" v-bind:key="idx">
        <h6>{{ res.n }}</h6>
        <p class="ml-4">{{ parseFloat(res.v).toFixed(10) }}</p>
    </v-container>

    <v-icon 
        class="ic-c"
        large
        left
        @click="() => {open = false}"
      >
        mdi-close-circle-outline
      </v-icon>

    </v-card>

    <v-btn v-if="!open" :color="color" class=" color-wt" @click="() => {open = true}">
        {{ name }}
    </v-btn>
    
   
</div>
</template>

<script>
export default {
    name: 'ConvertMulti',
    data () {
        return {
            name: 'Sigma',
            color: '#495057',
            open: false,
            input: [{n: "resistor", v: 0}, 
                    {n: "indutor", v: 0}, 
                    {n: "capacitor", v: 0} 
                    ],
        }
    },
    computed: {
        calculo() {


            return [{n: 'Valor sigma', v: 30.000}, 
                    {n: 'valor sigma ao quadrado', v: 60},
                    ];
        }
    }
}
</script>

<style scoped>
.color-wt {
    color: white;
}
.cl-btn {
    color: #26c6da;
}
.bg-blue1 {
    background-color: #26c6da;
}
.input-cl {
    background-color: white;
    border-radius: 10px;
    height: 30px;
    width: 90%;
    -webkit-appearance: none; 
}

input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
  margin: 0; 
}

.lc {
    text-transform: lowercase;
}

.result {
    width: 95%;
    background-color: white;
    color: black;
    line-height: 2;
}

.ic-c {
    color: white;
    cursor: pointer;
    margin: 10px 44%;
}

</style>
