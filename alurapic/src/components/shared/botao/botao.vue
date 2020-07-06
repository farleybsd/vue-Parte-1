<template>
  <button @click="(disparaAcao())" :class="estilodoBotao" class="botao" :type="tipo">{{rotulo}}</button>
</template>


<script>
export default {
  props: {
    tipo: {
      required: true,
      type: String
    },
    rotulo: {
      required: true,
      type: String
    },
    confirmacao: Boolean,
    estilo: String
  },
  methods: {
    disparaAcao() {
      if (this.confirmacao) {
        if (confirm("Confirma operacao?")) {
          //this.$emit("botaoAtivado", new Date());
          this.$emit("botaoAtivado");
        }

        return;
      }
      //this.$emit("botaoAtivado", new Date());
      this.$emit("botaoAtivado");
    }
  },
  computed: {
    estilodoBotao() {
      if (this.estilo == "padrao" || !this.estilo) return " botao-padrao";
      if (this.estilo == "perigo") return " botao-perigo";
    }
  }
};
</script>

<style  scoped>
botao {
  display: inline-block;
  padding: 10px;
  border-radius: 3px;
  margin: 10px;
  font-size: 1.2em;
}

.botao-perigo {
  background: firebrick;
  color: white;
}

.botao-padrao {
  background: darkcyan;
  color: white;
}
</style>
