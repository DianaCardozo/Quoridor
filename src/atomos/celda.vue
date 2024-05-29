<template>
    <div class = "celda" :class="celdaClass" @click="ControlClick"></div>
</template>
  
  <script>
  export default {
    props: {
      IndexRow: Number,
      Indexcelda: Number,
      Jugador1Posicion: Object,
      Jugador2Posicion: Object,
      TurnoJugador: Number,
      Bloqueoceldas: Array,
      ActivarControlCelda: Boolean,
      MovimientoJugador: Function,
      ControlClickCelda: Function,
      CeldaBloqueo: Function,
      ConfirmacionMovimiento : Function,
      Marca1: Function,
      Marca2: Function
    },
    computed: {
      celdaClass() {
        const isjugador1 = this.PosicionJugador1.row === this.rowIndex && this.PosicionJugador1.column === this.celdaIndex;
        const isjugador2 = this.PosicionJugador2.row === this.rowIndex && this.PosicionJugador2.column === this.celdaIndex;
        const isBloqueo = this.Bloqueoceldas.some(Bloqueo => Bloqueo.row === this.rowIndex && Bloqueo.column === this.celdaIndex);
        const ismovible = (this.TurnoJugador === 1 && this.Marcar1(this.rowIndex, this.celdaIndex)) || (this.TurnoJugador === 2 && this.Marcar2(this.rowIndex, this.celdaIndex));
  
        return {
          'celda--inicio': this.rowIndex === 0 || this.rowIndex === 8,
          'celda--ColorBase': this.rowIndex != 0 && this.rowIndex != 8,
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
        this.BloquearCelda(this.rowIndex, this.celdaIndex);
        this.MovimientoJugador(this.rowIndex, this.celdaIndex);
        this.ControlClickCelda(this.rowIndex, this.celdaIndex);
      }
    }
  };
  </script>
  
  <style scoped>
  /* Bloque */
  /* /* .celda {
    width: 70px;
    height: 70px;
    border: 0.5px solid #72b0f7;
  }  
   */
   .celda {
  width: 80px; /* Aumentar el ancho */
  height: 80px; /* Aumentar la altura */
  border: 1px solid #72f7c4; /* Ajustar el grosor y el color del borde */
}
  /* Modificador */
  /* .celda--inicio {
    background-color: lightblue;
  } */
  .celda--inicio {
  background-color: rgb(171, 255, 145); /* Color de fondo para celda de inicio */
}
  /* .celda--ColorBase {
    background-color: #33659e;
  } */
  .celda--ColorBase {
  background-color:  #2c5234; /* Nuevo color base */
}
/* 
  .celda--jugador1 {
    background-color: red;
  } */
  .celda--jugador1 {
  background-color: #940a8d; /* Nuevo color para jugador 1 */
}

  .celda--jugador2 {
    background-color: #f35dcd;
  }

  .celda--movible {
    opacity: 0.7;
  }

  .celda--deshabilitado {
    pointer-events: none;
    opacity: 0.6;
  }

  .celda--bloqueada {
    background-color: #333;
  } 
  </style>