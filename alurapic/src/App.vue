<template>
  <div>
    <h1>{{titulo}}</h1>

    <ul>
      <li v-for="foto of fotos">
        <img :src="foto.url" v-bind:alt="foto.titulo" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
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
</style>
