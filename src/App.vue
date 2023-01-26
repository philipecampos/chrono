<template>
  <v-app>
    <v-main>
      <v-row no-gutters>
        <v-col cols="3">
          <BarraLateral />
        </v-col>
        <v-col class="" cols="9">
          <Formulario @salvar-tarefa="salvarTarefa" />
          <Tarefa :tarefas="tarefas" />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BarraLateral from '@/components/BarraLateral.vue'
import Formulario from '@/components/Formulario.vue'
import ITarefa from '@/interfaces/ITarefa'
import Tarefa from '@/components/Tarefa.vue'

export default defineComponent({
  name: 'App',
  components: {
    Tarefa,
    Formulario,
    BarraLateral,
  },
  data() {
    return {
      tarefas: [] as Array<ITarefa>,
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
  },
})
</script>
