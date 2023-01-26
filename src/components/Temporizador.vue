<template>
  <div class="d-flex justify-lg-space-between align-center">
    <Cronometro :tempo-em-segundos="tempoEmSegundos" />
    <v-btn-group density="comfortable">
      <v-btn :prepend-icon="botaoAtivo.icone" class="border" @click="iniciar">
        <template #prepend>
          <v-icon class="" color="primary" size="x-large"></v-icon>
        </template>
        {{ botaoAtivo.texto }}
      </v-btn>
      <v-btn
        :disabled="!cronometroAtivo"
        class="border"
        dark
        @click="finalizar"
      >
        <template #prepend>
          <v-icon color="primary" size="x-large">mdi-stop</v-icon>
        </template>
        Stop
      </v-btn>
    </v-btn-group>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Cronometro from '@/components/Cronometro.vue'

export default defineComponent({
  name: 'Temporizador',
  components: { Cronometro },
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
      },
    }
  },
  computed: {
    botaoAtivo() {
      return this.cronometroAtivo ? this.botaoPause : this.botaoPlay
    },
  },
  methods: {
    iniciar() {
      if (this.cronometroAtivo) {
        this.interromper()
        return
      }

      //1 seg = 1000 ms
      this.cronometroAtivo = true
      this.cronometro = window.setInterval(() => {
        this.tempoEmSegundos += 1
      }, 1000)
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
    },
  },
})
</script>

<style scoped></style>
