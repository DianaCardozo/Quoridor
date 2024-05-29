<script>
import ModalWinner from './modal.vue'

export default {
  components: {
    ModalWinner
  },
  data() {
    return {
      board: [],
      player1Position: { row: 0, column: 4 },
      player2Position: { row: 8, column: 4 },
      currentPlayer: 1,
      selectedCell: null,
      showWinnerModal: false,
      winner: null
    };
  },
  mounted() {
    // Create 8x8 chess board
    for (let i = 0; i < 9; i++) {
      let row = [];
      for (let j = 0; j < 9; j++) {
        row.push({});
      }
      this.board.push(row);
    }
    window.addEventListener('keydown', this.movePlayer);
  },
    beforeDestroy() {
    // Elimina el event listener antes de destruir el componente para evitar problemas de memoria
    window.removeEventListener('keydown', this.movePlayer);
  },
// //   methods: {
// //     movePlayer(event) {
// //       const { row, column } = this.playerPosition;
// //       switch (event.key) {
// //         case 'ArrowUp':
// //           if (row > 0 && this.canMoveTo(row - 1, column))
// this.playerPosition.row--;
// //           break;
// //         case 'ArrowDown':
// //           if (row < 7 && this.canMoveTo(row + 1, column))
// this.playerPosition.row++;
// //           break;
// //         case 'ArrowLeft':
// //           if (column > 0 && this.canMoveTo(row, column - 1))
// this.playerPosition.column--;
// //           break;
// //         case 'ArrowRight':
// //           if (column < 7 && this.canMoveTo(row, column + 1))
// this.playerPosition.column++;
// //           break;
// //       }
// //     },
// //  canMoveTo(row, column) {
//     //   const { playerPosition } = this;
//     //   const { row: playerRow, column: playerColumn } = playerPosition;
//     //   return (
//     //     (row === playerRow && Math.abs(column - playerColumn) ===
// 1) || // Comprueba si está en la misma fila y una columna de distancia
//     //     (column === playerColumn && Math.abs(row - playerRow) ===
// 1)     // Comprueba si está en la misma columna y una fila de
// distancia
// //       );
// //     }
// //   }
// // }
methods: {
    movePlayer(row, column) {

      if ((this.currentPlayer === 1 && this.canMoveTo(this.player1Position.row, this.player1Position.column,row, column)) ||
          (this.currentPlayer === 2 && this.canMoveTo(this.player2Position.row, this.player2Position.column, row, column))) {
        if (this.currentPlayer === 1) {
          this.player1Position.row = row;
          this.player1Position.column = column;
          this.currentPlayer = 2; // Cambiar al jugador 2
        } else {
          this.player2Position.row = row;
          this.player2Position.column = column;
          this.currentPlayer = 1; // Cambiar al jugador 1
        }
    }
    if (this.player1Position.row === this.board.length - 1) {
        this.showWinnerMessage(1);
      } else if (this.player2Position.row === 0) {
        this.showWinnerMessage(2);
      }
    },
    canMoveTo(currentRow, currentColumn, row, column) {
      const rowDiff = Math.abs(row - currentRow);
      const columnDiff = Math.abs(column - currentColumn);
      return (
        (rowDiff === 1 && columnDiff === 0) || // Mover arriba o abajo
        (rowDiff === 0 && columnDiff === 1) // Mover izquierda o derecha
      );
    },

    selectCell(row, column) {
      this.selectedCell = { row, column };
    },

    Marcar1(row, column){
    const { player1Position: player1Position } = this;
    const { row: player1Row, column: player1Column } = player1Position;

      return (
        (row === player1Row && Math.abs(column - player1Column) === 1)
|| // Comprueba si está en la misma fila y una columna de distancia
        (column === player1Column && Math.abs(row - player1Row) === 1)
      )
    },
    Marcar2(row, column){
    const { player2Position: player2Position } = this;
    const { row: player2Row, column: player2Column } = player2Position;

      return (
        (row === player2Row && Math.abs(column - player2Column) === 1)
|| // Comprueba si está en la misma fila y una columna de distancia
        (column === player2Column && Math.abs(row - player2Row) === 1)
      )
    },
    showWinnerMessage(player) {
      this.winner = player;
      this.showWinnerModal = true;
    },
  resetGame() {
      // Restablecer las posiciones de los jugadores
      this.player1Position = { row: 0, column: 4 };
      this.player2Position = { row: 8, column: 4 };

      // Limpiar la celda seleccionada
      this.selectedCell = { row: null, column: null };

      // Reiniciar el turno del jugador
      this.currentPlayer = 1;

      this.showWinnerModal = false;
    }
  }
}
</script>

<template>
  <div class="board-container"  @keydown="movePlayer">
      <div class="board">
        <div v-for="(row, rowIndex) in board" :key="rowIndex" class="row" :class="{ 'first-row': rowIndex === 0 }">
          <div v-for="(cell, cellIndex) in row" :key="cellIndex"
                  class="cell" :class="{ 'inicio': rowIndex === 0 || rowIndex === 8 ,
                  'cellColor':  rowIndex != 0 & rowIndex != 8,
                  'player1': player1Position.row === rowIndex && player1Position.column === cellIndex,
                  'player2': player2Position.row === rowIndex && player2Position.column === cellIndex,
                  'disabled': (currentPlayer === 1 && player2Position.row === rowIndex && player2Position.column === cellIndex)
                   || (currentPlayer === 2 && player1Position.row === rowIndex && player1Position.column === cellIndex),
                  'movable': (currentPlayer === 1 && Marcar1(rowIndex, cellIndex)) || (currentPlayer === 2 && Marcar2(rowIndex, cellIndex)),
                  'selected': this.selectedCell && this.selectedCell.row === rowIndex && this.selectedCell.column === cellIndex}"
                  @click="movePlayer(rowIndex, cellIndex), selectCell(rowIndex, cellIndex)">
                  <ModalWinner v-if="showWinnerModal" :winner="winner" @reset="resetGame" />
          </div>
        </div>
      </div>
    </div>
</template>

<style scoped>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.board-container {
display: flex;
justify-content: center;
align-items: center;
height: 90vh;
flex: content;
}

.board {
  display: flex;
  flex-wrap: wrap;
  width: 560px;
  height: 560px;
}

.row {
  display: flex;
}

.cell {
  width: 70px;
  height: 70px;
  border: 0.5px solid #72b0f7;
}

.inicio {
  background-color: lightblue;
}

.cellColor {
  background-color: #33659e;
}

.selected {
  border-color: yellow; /* Color del borde de la celda seleccionada */
}

.player1 {
  background-color: red; /* Color del primer jugador */
}

.player2{
    background-color: rgb(255, 162, 0);
}

.movable {
  opacity: 0.6; /* Color de las casillas a las que se puede mover */
}

.disabled {
  pointer-events: none; /* Deshabilita los clics en las celdas */
  opacity: 0.5; /* Reduce la opacidad de las celdas */
}
</style>
