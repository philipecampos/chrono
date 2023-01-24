<template>
  <div class="d-flex justify-lg-space-between align-center">
    <Cronometro :tempo-em-segundos="tempoEmSegundos"/>
    <v-btn-group>
      <v-btn
        :prepend-icon="botaoAtivo.icone"
        class="border play"
        @click="iniciar">
        <template v-slot:prepend>
          <v-icon color="primary">{{ botaoAtivo.icone }}</v-icon>
        </template>
        {{ botaoAtivo.texto }}
      </v-btn>
      <v-btn
        dark
        :disabled="!cronometroAtivo"
        class="play"
        @click="finalizar">
        <template v-slot:prepend>
          <v-icon color="primary">mdi-stop</v-icon>
        </template>
        Stop
      </v-btn>
    </v-btn-group>

  </div>
</template>

<script lang="ts">
import {defineComponent} from "vue"
import Cronometro from "@/components/Cronometro.vue";

export default defineComponent({
  name: "Temporizador",
  components: {Cronometro},
  emits: ['temporizadorFinalizado'],
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroAtivo: false,
      textoBotao: 'Play',
      botaoPlay: {
        texto: 'Play',
        icone: 'mdi-play',
      },
      botaoPause: {
        texto: 'Pause',
        icone: 'mdi-pause',
      }
    }
  },
  computed: {
    botaoAtivo() {
      return this.cronometroAtivo ? this.botaoPause : this.botaoPlay
    }
  },
  methods: {
    iniciar() {
      if (this.cronometroAtivo) {
        this.interromper()
        return;
      }

      //1 seg = 1000 ms
      this.cronometroAtivo = true
      this.cronometro = window.setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    interromper() {
      this.cronometroAtivo = false
      clearInterval(this.cronometro)
    },
    finalizar() {
      this.cronometroAtivo = false
      clearInterval(this.cronometro)
      this.$emit('temporizadorFinalizado', this.tempoEmSegundos)
      this.tempoEmSegundos = 0
    }
  },
})
</script>

<style scoped>
.play {
  min-width: 7rem;
}
</style>
