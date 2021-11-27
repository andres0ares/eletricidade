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

    <v-btn :color="color" class=" color-wt" @click="calcularS">
        Calcular s1 e s2
    </v-btn>

    <v-container class="result ma-2" v-if="superamortecido.itIs">
        <h6>Circuito superamortecido</h6><br>
        <h6>valor do s1:</h6>
        <p class="ml-4">{{ parseFloat(superamortecido.s1).toFixed(10) }}</p>
        <h6>valor do s2:</h6>
        <p class="ml-4">{{ parseFloat(superamortecido.s2).toFixed(10) }}</p>
    </v-container>

    <v-container class="result ma-2" v-if="subamortecido.itIs">
        <h6>Circuito subamortecido</h6><br>
        <h6>valor do s1:</h6>
        <p class="ml-4">{{ subamortecido.s1 }}</p>
        <h6>valor do s2:</h6>
        <p class="ml-4">{{ subamortecido.s2 }}</p>
    </v-container>

    <v-container class="result ma-2" v-if="criticamenteAmortecido.itIs">
        <h6>Circuito criticamente amortecido</h6><br>
        <h6>valor do s1:</h6>
        <p class="ml-4">{{ criticamenteAmortecido.s1 }}</p>
        <h6>valor do s2:</h6>
        <p class="ml-4">{{ criticamenteAmortecido.s2 }}</p>
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
    name: 'RlcEmParalelo',
    data () {
        return {
            name: 'RLC Em Paralelo',
            color: '#52796f',
            open: false,
            input: [{n: "resistor", v: 0}, 
                    {n: "indutor", v: 0}, 
                    {n: "capacitor", v: 0} 
            ],
            superamortecido: {itIs: false, s1: 0, s2: 0},
            subamortecido: {itIs: false, s1: '', s2: ''},
            criticamenteAmortecido: {itIs: false, s1: 0, s2: 0}
        }
    },
    computed: {
        calculo() {

            let [R, L, C] = this.input;

            let sigma = 1 / (2* R.v * C.v);
            let sigma2 = sigma * sigma;

            let omega = 1 / (Math.sqrt(L.v * C.v));
            let omega2 = omega * omega

            


            return [{n: 'Valor sigma', v: sigma}, 
                    {n: 'valor sigma ao quadrado', v: sigma2},
                    {n: 'valor de omega 0', v: omega},
                    {n: 'valor de omega 0 ao quadrado', v: omega2}
                    ];
        }
    },
    methods: {
        calcularS () {

            let [R, L, C] = this.input;

            let sigma = 1 / (2* R.v * C.v);
            let sigma2 = sigma * sigma;

            let omega = 1 / (Math.sqrt(L.v * C.v));
            let omega2 = omega * omega

            let s1 = `-\\left(\\frac{1}{2\\cdot \\:\\left(${R.v}\\right)\\:\\left(${C.v}\\right)}\\right)\\:+\\sqrt{\\left(\\frac{1}{2\\cdot \\left(${R.v}\\right)\\:\\:\\left(${C.v}\\right)}\\right)^2-\\left(\\frac{1}{\\sqrt{\\left(${L.v}\\right)\\left(${C.v}\\right)}}\\right)^2}`;
            let s2 = `-\\left(\\frac{1}{2\\cdot \\:\\left(${R.v}\\right)\\:\\left(${C.v}\\right)}\\right)\\:-\\sqrt{\\left(\\frac{1}{2\\cdot \\left(${R.v}\\right)\\:\\:\\left(${C.v}\\right)}\\right)^2-\\left(\\frac{1}{\\sqrt{\\left(${L.v}\\right)\\left(${C.v}\\right)}}\\right)^2}`;

            //calcular s1 e s2
            if(sigma2 > omega2) {
                this.subamortecido.itIs = false;
                this.criticamenteAmortecido.itIs = false;

                this.superamortecido.s1 = (sigma * -1) + Math.sqrt(sigma2 - omega2);
                this.superamortecido.s2 = (sigma * -1) - Math.sqrt(sigma2 - omega2);
                this.superamortecido.itIs = true;
            }else if (sigma2 < omega2){
                this.superamortecido.itIs = false;
                this.criticamenteAmortecido.itIs = false;

                this.subamortecido.s1 = s1;
                this.subamortecido.s2 = s2;
                this.subamortecido.itIs = true;
            }else {
                this.subamortecido.itIs = false;
                this.superamortecido.itIs = false;

                this.criticamenteAmortecido.s1 = sigma * -1;
                this.criticamenteAmortecido.s2 = sigma * -1;
                this.criticamenteAmortecido.itIs = true;
            }
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
