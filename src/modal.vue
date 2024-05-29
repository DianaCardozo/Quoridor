
  <script>
  export default {
    props: {
      winner: Number
    },
    data() {
      return {
        showModal: true
      };
    },
    methods: {
      closeModal() {
        this.showModal = false;
      },
      resetGame() {
        this.$emit('reset');
        this.closeModal();
      }
    }
  }
  </script>

  <template>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <p>¡Ganaste jugador {{ winner }}!</p>
        <button @click="resetGame">Reiniciar</button>
      </div>
    </div>
  </template>
  
  <style scoped>
.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #1a1a1d;
  padding: 20px;
  border: 2px solid #c3073f;
  border-radius: 10px;
  width: 80%;
  max-width: 500px;
  text-align: center;
  color: white;
  font-family: 'Arial', sans-serif;
  animation: fadeIn 0.5s;
}

.close {
  color: #c3073f;
  float: right;
  font-size: 28px;
  font-weight: bold;
  cursor: pointer;
}

.close:hover,
.close:focus {
  color: #ff6f61;
  text-decoration: none;
  cursor: pointer;
}

.reset-button {
  background-color: #c3073f;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.reset-button:hover {
  background-color: #ff6f61;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
  </style>