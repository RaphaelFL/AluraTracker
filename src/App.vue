<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAterado="trocaTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioComponents @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaComponents v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <BoxComponents v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </BoxComponents>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue'
import FormularioComponents from './components/Formulario.vue'
import TarefaComponents from './components/Tarefa.vue'
import BoxComponents from './components/Box.vue'
import ITarefa from './Interfaces/ITarefa'

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioComponents,
    TarefaComponents,
    BoxComponents
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocaTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>