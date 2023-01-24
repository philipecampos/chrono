<template>
  <v-list
    class="mt-3">
    <v-list-item
      v-for="(tarefa, index) in tarefas"
      :key="index"
      class="bg-amber-lighten-5 mx-3 my-n2"
      link>
      <v-row>
        <v-col cols="7">{{ tarefa.descricao }}</v-col>
        <v-col>
          <Cronometro :tempo-em-segundos="15"/>
        </v-col>
      </v-row>
    </v-list-item>
  </v-list>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue"
import Cronometro from "@/components/Cronometro.vue"
import ITarefa from "@/interfaces/ITarefa";

export default defineComponent({
  components: {Cronometro},
  name: "Tarefa",
  props: {
    Tarefas: Array<ITarefa>
  },
  setup() {

  }
})
</script>

<style scoped>

</style>
