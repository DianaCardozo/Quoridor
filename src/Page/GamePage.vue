<template>
    <PlantillaJuego
      :Tablero="Tablero"
      :PosicionJugador1="PosicionJugador1"
      :PosicionJugador2="PosicionJugador2"
      :TurnoJugador="TurnoJugador"
      :Bloqueoceldas="Bloqueoceldas"
      :ControldeCeldaActivado="ControldeCeldaActivado"
      :MostrarGanadorModal="MostrarGanadorModal"
      :ganador="ganador"
      :MovimientoJugador="MovimientoJugador"
      :ControlClickCelda="ControlClickCelda"
      :BloquearCelda="BloquearCelda"
      :SePuedeMover="SePuedeMover"
      :Marcar1="Marcar1"
      :Marcar2="Marcar2"
      :ReiniciarJuego="ReiniciarJuego"
    />
  </template>
  
  <script>
  import PlantillaJuego from '../plantillas/PlantillaJuego.vue';
  
  export default {
    components: {
      PlantillaJuego
    },
    data() {
      return {
        Tablero: [],
        PosicionJugador1: { row: 0, column: 4 },
        PosicionJugador2: { row: 8, column: 4 },
        TurnoJugador: 1,
        MostrarGanadorModal: false,
        ganador: null,
        Contador1: 0,
        Contador2: 0,
        ControldeCeldaActivado: false,
        Bloqueoceldas: []
      };
    },
    mounted() {
      for (let i = 0; i < 9; i++) {
        let row = [];
        for (let j = 0; j < 9; j++) {
          row.push({});
        }
        this.Tablero.push(row);
      }
    },
    methods: {
      MovimientoJugador(row, column) {
        if ((this.TurnoJugador === 1 && this.SePuedeMover(this.PosicionJugador1.row, this.PosicionJugador1.column, row, column)) ||
          (this.TurnoJugador === 2 && this.SePuedeMover(this.PosicionJugador2.row, this.PosicionJugador2.column, row, column))) {
          if (this.TurnoJugador === 1) {
            this.PosicionJugador1.row = row;
            this.PosicionJugador1.column = column;
            this.TurnoJugador = 2;
          } else {
            this.PosicionJugador2.row = row;
            this.PosicionJugador2.column = column;
            this.TurnoJugador = 1;
          }
        }
        if (this.PosicionJugador1.row === this.Tablero.length - 1) {
          this.showganadorMessage(1);
        } else if (this.PosicionJugador2.row === 0) {
          this.showganadorMessage(2);
        }
      },
      ControlClickCelda(row, column) {
        if (this.ControldeCeldaActivado == true) {
          this.ControldeCeldaActivado = false;
        } else if (this.TurnoJugador === 1 && this.PosicionJugador1.row === row && this.PosicionJugador1.column === column) {
          this.ControldeCeldaActivado = true;
          this.BloquearCelda(row, column);
        } else if (this.TurnoJugador === 2 && this.PosicionJugador2.row === row && this.PosicionJugador2.column === column) {
          this.ControldeCeldaActivado = true;
          this.BloquearCelda(row, column);
        }
      },
      BloquearCelda(row, column) {
        if (this.ControldeCeldaActivado == true) {
          const index = this.Bloqueoceldas.findIndex(selected => selected.row === row && selected.column === column);
          if (!(this.PosicionJugador1.row === row && this.PosicionJugador1.column === column || this.PosicionJugador2.row === row && this.PosicionJugador2.column === column)) {
            if (this.TurnoJugador === 1 && this.Contador1 < 8 && index === -1) {
              this.Bloqueoceldas.push({ row, column });
              this.Contador1++;
              this.TurnoJugador = 2;
              this.ControldeCeldaActivado = false;
            } else if (this.TurnoJugador === 2 && this.Contador2 < 8 && index === -1) {
              this.Bloqueoceldas.push({ row, column });
              this.Contador2++;
              this.TurnoJugador = 1;
              this.ControldeCeldaActivado = false;
            }
          }
        }
      },
      SePuedeMover(currentrow, currentcolumn, row, column) {
        const rowDiff = Math.abs(row - currentrow);
        const columnDiff = Math.abs(column - currentcolumn);
        const isCellSelected = this.Bloqueoceldas.some(selected => selected.row === row && selected.column === column);
        return (
          (rowDiff === 1 && columnDiff === 0 && !isCellSelected) ||
          (rowDiff === 0 && columnDiff === 1 && !isCellSelected)
        );
      },
      Marcar1(row, column) {
        const { PosicionJugador1 } = this;
        const { row: player1row, column: player1column } = PosicionJugador1;
        const isCellSelected = this.Bloqueoceldas.some(selected => selected.row === row && selected.column === column);
        return (
          (row === player1row && Math.abs(column - player1column) === 1 && !isCellSelected) ||
          (column === player1column && Math.abs(row - player1row) === 1 && !isCellSelected)
        );
      },
      Marcar2(row, column) {
        const { PosicionJugador2 } = this;
        const { row: player2row, column: player2column } = PosicionJugador2;
        const isCellSelected = this.Bloqueoceldas.some(selected => selected.row === row && selected.column === column);
        return (
          (row === player2row && Math.abs(column - player2column) === 1 && !isCellSelected) ||
          (column === player2column && Math.abs(row - player2row) === 1 && !isCellSelected)
        );
      },
      showganadorMessage(player) {
        this.ganador = player;
        this.MostrarGanadorModal = true;
      },
      ReiniciarJuego() {
        this.PosicionJugador1 = { row: 0, column: 4 };
        this.PosicionJugador2 = { row: 8, column: 4 };
        this.TurnoJugador = 1;
        this.MostrarGanadorModal = false;
        this.Contador1 = 0;
        this.Contador2 = 0;
        this.Bloqueoceldas = [];
      }
    }
  };
  </script>
  
  <style scoped>
  * {
    margin: 0;
    padding: 0;
  }
  
  .seleccionar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(177, 94, 255, 0.5);
    opacity: 0.6;
    overflow: hidden;
  }

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