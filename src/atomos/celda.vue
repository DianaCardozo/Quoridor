<template>
  <div class="tablero">
    <div class="celda" :class="celdaClass" @click="ControlClick"></div>
  </div>
</template>

<script>

export default {
  components: {
    InstruccionesModal
  },
  props: {
    indexRow: Number,
    celdaIndex: Number,
    Jugador1Posicion: Object,
    Jugador2Posicion: Object,
    TurnoJugador: Number,
    Bloqueoceldas: Array,
    ControlCeldaActivo: Boolean,
    MovimientoJugador: Function,
    ControlClickCelda: Function,
    BloquearCelda: Function,
    SePuedeMover: Function,
    Marcar1: Function,
    Marcar2: Function
  },
  data() {
    return {
      mensaje: '',
      mostrarModal: false
    };
  },
  computed: {
    celdaClass() {
      const isjugador1 = this.Jugador1Posicion.row === this.indexRow && this.Jugador1Posicion.column === this.celdaIndex;
      const isjugador2 = this.Jugador2Posicion.row === this.indexRow && this.Jugador2Posicion.column === this.celdaIndex;
      const isBloqueo = this.Bloqueoceldas.some(Bloqueo => Bloqueo.row === this.indexRow && Bloqueo.column === this.celdaIndex);
      const ismovible = (this.TurnoJugador === 1 && this.Marcar1(this.indexRow, this.celdaIndex)) || (this.TurnoJugador === 2 && this.Marcar2(this.indexRow, this.celdaIndex));

      return {
        'celda--inicio': this.indexRow === 0 || this.indexRow === 8,
        'celda--ColorBase': this.indexRow != 0 && this.indexRow != 8,
        'celda--jugador1': isjugador1,
        'celda--jugador2': isjugador2,
        'celda--deshabilitado': (this.TurnoJugador === 1 && isjugador2) || (this.TurnoJugador === 2 && isjugador1),
        'celda--movible': ismovible,
        'celda--bloqueada': !isjugador1 && !isjugador2 && isBloqueo
      };
    }
  },
  methods: {
    ControlClick() {
      this.BloquearCelda(this.indexRow, this.celdaIndex);
      this.MovimientoJugador(this.indexRow, this.celdaIndex);
      this.ControlClickCelda(this.indexRow, this.celdaIndex);
      this.mostrarMensaje();
    },
    mostrarMensaje() {
      if (this.TurnoJugador === 1) {
        this.mensaje = 'Jugador 1, mueve tu ficha';
      } else {
        this.mensaje = 'Jugador 2, mueve tu ficha';
      }
      setTimeout(() => {
        this.mensaje = '';
      }, 2000);
    }
  }
};
</script>

<style scoped>
.tablero {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #006400; /* Verde oscuro */
  padding: 20px;
  border-radius: 10px;
}

.celda {
  width: 70px;
  height: 70px;
  border: 2px solid #d4af37; /* Borde dorado */
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  border-radius: 50%; /* Forma redonda */
}

.mensaje {
  position: absolute;
  top: -25px;
  background-color: #fffbea;
  color: #d4af37;
  border: 1px solid #d4af37;
  padding: 5px;
  border-radius: 3px;
  font-size: 12px;
}

/* Modificador */
.celda--inicio {
  background-color: #fff8dc; /* Fondo dorado claro */
}

.celda--ColorBase {
  background-color: #fffbea; /* Fondo dorado muy claro */
}

.celda--jugador1 {
  background-color: #4b0082; /* Morado oscuro */
}

.celda--jugador2 {
  background-color: #dda0dd; /* Morado suave */
}

.celda--deshabilitado {
  background-color: #c5c5c5; /* Gris */
}

.celda--movible {
  border-color: #daa520; /* Dorado intenso */
}

.celda--bloqueada {
  background-color: #8b4513; /* Marrón oscuro */
}

.btn-instrucciones {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #ffd700;
  color: #4b0082;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.btn-instrucciones:hover {
  background-color: #e5c100;
}
</style>
