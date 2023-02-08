<template>
    <div class="conversor">
        <h2 class="coin-name">
            <img :src="moedaA.img" class="flag" alt="bandeira do país">
            {{ moedaA.fiat }} <icon>&#8646;</icon> {{ moedaB.fiat }}
            <img :src="moedaB.img" class="flag" alt="bandeira do país">
        </h2>
        <input class="input" type="text" v-model="moedaA_value" v-bind:placeholder="moedaA.fiat">
        <button class="button" v-on:click="converter">Converter</button>
        <h2 class="conversion-result">{{ moedaB_value }}</h2>
    </div>
</template>

<script>
export default  { 
    name: "ConversorVue",
    props: ['moedaA', 'moedaB'],
    data(){
        return{
            moedaA_value:"",
            moedaB_value:0
        }
    },
    methods: {
        converter(){
            let de_para = this.moedaA.fiat + "_" + this.moedaB.fiat;
            let url = "https://free.currconv.com/api/v7/convert?q="+
            de_para
            +"&compact=ultra&apiKey=1b24d1525b41c3d2b5ea"

            fetch(url).then(res => {
                return res.json();
                    })
                    .then(json =>{
                        let cotacao = json[de_para];
                        this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2)
                    })
        }
    }
}
</script>

<style scoped>
.button{
    background-color: rgb(15, 220, 80);
    font-weight: 300;
    height: 1.9rem;
}
.conversor{
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    font-size: 1.5rem;
    max-width: 300px;
    padding: 15px;
}
.coin-name{
    border: #000000 solid 1px;
    border-radius: 20px;
    font-size: 1.5rem;
    margin-bottom: 10px;
    padding: 5px 0;

}
.conversion-result{
    padding-top: 10px;
}
.flag{
    max-width: 30px;
    margin: auto;
}
.input{
    height: 1.5rem;
}

</style>