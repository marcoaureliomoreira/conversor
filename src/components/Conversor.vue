<template>
    <div class="conversor">
        <h2>{{moedaA}} Para {{moedaB}}</h2>
        <input class="field-value" type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
        <input class="button-converter" type="button" value="Converter" v-on:click="converter">
        <h2>{{moedaB_value}}</h2>
    </div>
</template>

<script>
    export default {
        name: "Conversor",
        props: ["moedaA","moedaB"],
        data() {
            return {
                moedaA_value: "",
                moedaB_value: 0
            };
        },
        methods: {
            converter(){

                let de_para = this.moedaA + "_" + this.moedaB;

                let url = 
                "https://free.currencyconverterapi.com/api/v6/convert?q="+
                de_para
                +"&compact=ultra&apiKey=64c9a7f1e3890ae94921";

                fetch(url)
                    .then(res => {
                        return res.json();
                    })
                    .then(json => {
                        let cotacao = json[de_para].val;
                        this.moedaB_value = (contacao * parseFloat(this.moedaA_value)).toFixed(2);
                    });

                }
        }
    };

    
</script>

<style scoped>

.field-value {
    width: 150px;
    height: 30px;
    padding: 0px 10px 0px 10px;
    border-radius: 0;
    background-color: #ecf0f1;
    border: none;
    }

.button-converter {
    width: 70px;
    height: 30px;
    border-radius: none;
    background-color: #bdc3c7;
    border-color: #bdc3c7;
    border: 5px;
    }


</style>

