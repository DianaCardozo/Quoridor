<template>
  <div class="row">
    <celda
      v-for="(celda, celdaIndex) in row"
      :key="celdaIndex"
      :rowIndex="rowIndex"
      :celdaIndex="celdaIndex"
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
import celda from '../atomos/celda.vue';

export default {
  components: {
    celda
  },
  props: {
    row: Array,
    rowIndex: Number,
    PosicionJugador1: Object,
    PosicionJugador2: Object,
    TurnoJugador: Number,
    Bloqueoceldas: Array,
    ControlCeldaActivado: Boolean,
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
.row {
  display: flex;
}
</style>