<template>
  <div>
    <v-sheet
      class="pa-3 elevation-3">
      <v-row>
        <v-col aria-label="Formulário para criação de uma nova tarefa" cols="8" role="form">
          <v-text-field
            density="comfortable"
            hide-details
            label="Qual terafa você deseja iniciar?"
            v-model="descricao"
            variant="outlined"></v-text-field>
        </v-col>
        <v-col>
          <Temporizador @temporizador-finalizado="finalizarTarefa"/>
        </v-col>
      </v-row>
    </v-sheet>
  </div>
</template>

<script lang="ts">
import {defineComponent} from "vue"
import Temporizador from "@/components/Temporizador.vue";

export default defineComponent({
  name: "Formulario",
  emits: ['salvarTarefa'],
  components: {
    Temporizador
  },
  data() {
    return {
      descricao: '',
      tarefas: this.listaTarefas
    }
  },
  methods: {
    finalizarTarefa(tempoDecorrido: number): void {
      this.$emit('salvarTarefa', {
        duracaoEmSegundos: tempoDecorrido,
        descricao: this.descricao
      })
      this.descricao = ''
    }
  }
})
</script>

<style scoped>

</style>
