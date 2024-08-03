<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <Button @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando"/>
    <Button @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando"/>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue';
import Button from './Button.vue';

 
export default defineComponent({
  name: 'TemporizadorComponente',
  emits: ['aoTemporizadorFinalizado'],
  components: {
    Cronometro,
    Button,
  },
  data(){
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false
    }
  },
  methods: {
    iniciar() {
      this.cronometro = setInterval(() => {
        console.log('adiiconando mais 1')
        this.tempoEmSegundos += 1;
      }, 1000)
      this.cronometroRodando = true;
    },
    finalizar() {
      clearInterval(this.cronometro)
      this.cronometroRodando = false;
      this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
      this.tempoEmSegundos = 0;
    }
  }
})
</script>