<template>
    <div class="Tablero">
      <filasTablero
        v-for="(row, rowIndex) in Tablero"
        :key="rowIndex"
        :row="row"
        :rowIndex="rowIndex"
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
    </div>
  </template>
  
  <script>
  import filasTablero from '../moleculas/filasTablero.vue';
  
  export default {
    components: {
      filasTablero
    },
    props: {
      Tablero: Array,
      PosicionJugador1: Object,
      PosicionJugador2: Object,
      TurnoJugador: Number,
      Bloqueoceldas: Array,
      ControldeCeldaActivado: Boolean,
      MovimientoJugador: Function,
      ControlClickCelda: Function,
      BloquearCelda: Function,
      SePuedeMover: Function,
      Marcar1: Function,
      Marcar2: Function
    }
  };
  </script>
  
  <style scoped>
  /* Bloque */
  .Tablero {
    display: flex;
    flex-wrap: wrap;
    width: 600px;
    height: 600px;
  }
  </style>