<template>
    <h1 class="label-title">Cálculo do IMC</h1>
    <h2 class="label-subtitle">Digite seu peso e altura para calcular seu IMC</h2>

    <div class="div-imc">
        <span class="p-float-label">
            <InputText id="input-weight" type="text" v-model="weight" v-bind:disabled="imc" />
            <label for="input-weight">Peso</label>
        </span>
    </div> 

    <div class="div-imc">
        <span class="p-float-label">
            <InputText id="input-height" type="text" v-model="height" :disabled="imc" />
            <label for="input-height">Altura</label>
        </span>
    </div>

    <div class="div-imc" v-if="!imc">
        <Button label="Limpar" @click="clear()"/>
        <Button label="Calcular" @click="calculate()" class="button-calculate"/>
    </div>

    <div class="div-imc">
    </div>

    <div v-if="imc">
        <p class="label-result">Seu IMC é: {{imc}}</p>
        <p class="label-classification">A classificação do seu IMC é: {{classification}}</p>
        <Button label="Calcular Novamente" @click="clear()"/>
    </div>
    
</template>

<script>
export default {
    data(){
        return{
            weight: null,
            height: null,
            imc: null,
            classification: ""
        }
    },
    methods:{
        calculate: function(){
            this.imc = (this.weight / (this.height * this.height)).toFixed(2);
            //console.log(this.imc);
            if (this.imc < 18.5){
                this.classification = "Magro";
            }else if (this.imc < 25){
                this.classification = "Normal";
            }else if (this.imc < 30){
                this.classification = "Sobrepeso";
            }else if (this.imc < 35){
                this.classification = "Obesidade";
            }else{
                this.classification = "Obesidade Grave";
            }
        },
        clear: function(){
            this.weight = null,
            this.height = null,
            this.imc = null,
            this.classification = ""
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.div-imc{ 
    margin-top: 2rem;
}
.label-title{
    font-size: 2rem;
}
.label-subtitle{
    font-size: 1.1rem;
}
.label-result{
    font-size: 2rem;
}
.label-classification{
    font-size: 1.5rem;
}
.button-calculate{
    margin-left: 1rem !important ;
}
</style>
