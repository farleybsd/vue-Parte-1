<template>
  <div class="corpo">
    <h1 class="centralizado">{{titulo}}</h1>

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotos">
        <meu-painel :titulo="foto.titulo">
          <img class="imagem-responsiva" :src="foto.url" v-bind:alt="foto.titulo" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "./components/shared/painel/Paniel.vue";
export default {
  components: {
    "meu-painel": Painel
  },
  data() {
    return {
      titulo: "AluraPic",
      fotos: []
    };
  },
  created() {
    // alert("Criei o component");
    let promise = this.$http.get("http://localhost:3000/v1/fotos");
    promise
      .then(res => res.json())
      .then(fotos => ((this.fotos = fotos), err => console.log(err))); //this.fotos vem do data
  }
};
</script>

<style>
.corpo {
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}
.centralizado {
  text-align: center;
}
.lista-fotos {
  list-style: none;
}
.lista-fotos .lista-fotos-item {
  display: inline-block;
}
.imagem-responsiva {
  width: 100%;
}
</style>
