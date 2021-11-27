<template>
<div>

    <v-card
    class="mx-auto color-wt"
    color="#26c6da"
    max-width="400"
    v-if="open"

    >
    <v-card-title>
      <span class="text-h6 font-weight-light">converter múltiplo</span>
    </v-card-title>
    
    <v-btn @click="() => {btns = multiplos}" class="cl-btn ma-6" depressed>Múltiplo</v-btn>
    <v-btn @click="() => {btns = submultiplos}" class="cl-btn ma-6" depressed>submúltiplo</v-btn>
    
    <input class="input-cl ma-5" type="number" name="valor" id="valor" 
    @change="(test) => valor = test.target.value">    
    
    
    <v-btn v-for="(btn, index) in (btns)" v-bind:key="index" 
    class="cl-btn ma-2 lc" @click="() => {multi = btn.n}">
        {{ `10^${btn.n}; ${btn.t}` }}
    </v-btn>
     

    <div class="result">
        <p class="ml-4">{{ parseFloat(calculo).toFixed(multi < 0 ? multi * -1 : (multi < 1 ? multi : 0)) }}</p>
    </div>

    <v-icon 
        class="ic-c"
        large
        left
        @click="() => {open = false}"
      >
        mdi-close-circle-outline
      </v-icon>

    </v-card>

    <v-btn v-if="!open" class="bg-blue1 color-wt" @click="() => {open = true}">
        Múltiplo e submúltiplo
    </v-btn>
    
   
</div>
</template>

<script>
export default {
    name: 'TemplateExa',
    data () {
        return {
            valor: 0,
            items: ['Foo', 'Bar', 'Fizz', 'Buzz'],
            btns: [],
            submultiplos: [{n: -1, t: '(d)'}, {n: -2, t: '(c)'}, {n: -3, t: '(m)'},
                            {n: -6, t: '(u)'}, {n: -9, t: '(n)'}, {n: -12, t: '(p)'},
                            {n: -15, t: '(f)'}],
            multiplos: [{n: 1, t: '(da)'}, {n: 2, t: '(h)'}, {n: 3, t: '(k)'},
                        {n: 6, t: '(M)'}, {n: 9, t: '(G)'}, {n: 12, t: '(T)'},
                        {n: 15, t: '(P)'}],
            multi: 0,
            open: false
        }
    },
    computed: {
        calculo() {
            return this.valor * (10 ** this.multi);
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
    background-color: white;
    color: #26c6da;
    border: 4px solid #26c6da;
    height: 40px;
    line-height: 2;
}

.ic-c {
    color: white;
    cursor: pointer;
    margin: 10px 44%;
}

</style>
