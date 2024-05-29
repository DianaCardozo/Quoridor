<template>
    <div :class="{'seleccionar': ControldeCeldaActivado}">
      <div class="Tablero-container">
        <Tablero
          :Tablero="Tablero"
          :PosicionJugador1="PosicionJugador1"
          :PosicionJugador2="PosicionJugador2"
          :TurnoJugador="TurnoJugador"
          :Bloqueoceldas="Bloqueoceldas"
          :ControldeCeldaActivado="ControldeCeldaActivado"
          :MovimientoJugador="MovimientoJugador"
          :ControlClickCelda="ControlClickCelda"
          :BloquearCelda="BloquearCelda"
          :SePuedeMover="SePuedeMover"
          :Marcar1="Marcar1"
          :Marcar2="Marcar2"
        />
        <Modalganador v-if="MostrarGanadorModal" :ganador="ganador" @reset="ReiniciarJuego" />
      </div>
    </div>
  </template>
  
  <script>
  import Tablero from '../organismos/Tablero.vue';
  import Modalganador from '../organismos/modal.vue';
  
  export default {
    components: {
      Tablero,
      Modalganador
    },
    props: {
      Tablero: Array,
      PosicionJugador1: Object,
      PosicionJugador2: Object,
      TurnoJugador: Number,
      Bloqueoceldas: Array,
      ControldeCeldaActivado: Boolean,
      MostrarGanadorModal: Boolean,
      ganador: Number,
      MovimientoJugador: Function,
      ControlClickCelda: Function,
      BloquearCelda: Function,
      SePuedeMover: Function,
      Marcar1: Function,
      Marcar2: Function,
      ReiniciarJuego: Function
    }
  };
  </script>
  
  <style scoped>

  .Tablero-container {
    position: fixed;
    z-index: 1;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 90vw;
    height: 90vh;
    overflow: auto;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  </style>
  