<template>
  <div class="painel">
    <h2 class="painel-titulo" v-on:dblclick="visivel = !visivel">{{titulo}}</h2>
    <transition name="painel-fade">
      <div class="painel-conteudo" v-show="visivel">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["titulo"], //datapropsigual react
  data() {
    return {
      visivel: true
    };
  }
};
</script>
/*apenas para esse componnet*/
<style scoped>
/* estilo do painel */

.painel {
  padding: 0 auto;
  border: solid 2px grey;
  display: inline-block;
  margin: 5px;
  box-shadow: 5px 5px 10px grey;
  width: 200px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}

.painel .painel-titulo {
  text-align: center;
  border: solid 2px;
  background: lightblue;
  margin: 0 0 15px 0;
  padding: 10px;
  text-transform: uppercase;
}
* {
  box-shadow: 5px 5px 5px;
}
.painel-fade-enter,
.painel-fade-leave-active {
  opacity: 0;
}
.painel-fade-enter-active,
.painel-fade-leave-active {
  transition: opacity 0.4s;
}
</style>

/*
Slot
Quando o Vue renderiza nosso componente Painel em App, ele não entende que deve preservar tudo aquilo que esta entre as tags <meu-painel>.
 O Vue manipula aquela parte do DOM trocando-a pela renderização do nosso componente Painel. Para que isso seja possível, precisamos indicar no template de Painel a
 área que queremos considerar como um slot, ou seja, aquela área que recebera tudo aquilo que tiver dentro da tag <meu-painel>. Para isso, vamos alterar
  o template alurapic/src/components/shared/painel/Painel.vue e trocar a div conteúdo pelo componente slot. Nosso componente final fica assim:


painel-fade-enter // antes do elemento ser incluído ou removido, o estado atual
painel-fade-enter-active // quando o elemento esta sendo incluído
painel-fade-leave-active // quando o elemento esta sendo removido
*/
