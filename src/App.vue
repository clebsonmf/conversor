<template>
  <header class="header">
    <img src="/moeda.png" class="coin-header" alt="simbolo da moeda">
    <h1 class="title-app">Conversor de Moedas</h1>
  </header>
  <div class="app" id="app">
    <div class="line">
      <ConversorVue  v-for="fiatPair in fiatPairs" :key="`${ fiatPair.fiatA }-${fiatPair.fiatB}`" :moedaA="fiatJson[fiatPair.fiatA]" :moedaB="fiatJson[fiatPair.fiatB]"/>
      <br v-if="!(index%2)"/>
    </div>
 </div>
</template>

<script>
import ConversorVue from './components/ConversorVue.vue';
import FiatsJson from './assets/fiats.json';

export default {
  name: 'App',
  components:{
    ConversorVue
  },
  data() {
    return {
      fiatJson: FiatsJson,
      fiatPairs: [
        { fiatA: 'objUsd', fiatB: 'objBrl' },
        { fiatA: 'objBrl', fiatB: 'objUsd' },
        { fiatA: 'objCad', fiatB: 'objBrl' },
        { fiatA: 'objBrl', fiatB: 'objCad' },
        { fiatA: 'objEur', fiatB: 'objBrl' },
        { fiatA: 'objBrl', fiatB: 'objEur' }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
.coin-header{
  display: flex;
  max-width: 80px;
}
.header{
  display: flex;
  background-color: rgb(2, 2, 68);
  justify-content: center;
  margin-bottom: 20px;
  padding: 15px;
  width: auto;
}

.line{
  display: grid;
  justify-items: center;
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.line div {
  margin: 10px 0;
  border: 1px solid;
}

.title-app{
  text-align: center;
  padding: 20px;
  font-size: 2.5rem; 
  color:rgb(255, 255, 255)
}
</style>
