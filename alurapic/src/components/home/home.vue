<template>
  <div>
    <h1 class="centralizado">{{titulo}}</h1>
    <input
      type="search"
      class="filtro"
      v-on:input="filtro=$event.target.value"
      placeholder="filtre por parte do titulo"
    />

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo" />
          <meu-botao tipo="button" rotulo="Remover" @click.native="remover(foto)" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Paniel.vue";
import imagemResponsiva from "../shared/imagem-responsiva/imagemResponsiva.vue";
import Botao from "../shared/botao/botao.vue";
export default {
  components: {
    "meu-painel": Painel,
    "imagem-responsiva": imagemResponsiva,
    "meu-botao": Botao
  },
  data() {
    return {
      titulo: "AluraPic",
      fotos: [],
      filtro: ""
    };
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        // filtra a lista, por enquanto vamos retornar uma lista em branco
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.fotos.filter(foto => exp.test(foto.titulo));
        return [];
      } else {
        // se o campo estiver vazio, não filtramos, retornamos a lista
        return this.fotos;
      }
    }
  },

  methods: {
    remover(foto) {
      if (confirm("Confirmar operação ?")) {
        alert("Remover a foto!" + foto.titulo);
      }
    }
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
.centralizado {
  text-align: center;
}
.lista-fotos {
  list-style: none;
}
.lista-fotos .lista-fotos-item {
  display: inline-block;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
