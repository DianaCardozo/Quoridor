
  <script>
  export default {
    props: {
      ganador: Number
    },
    data() {
      return {
        MostrarModal: true
      };
    },
    methods: {
      resetGame() {
        this.$emit('reset');
      }
    }
  }
  </script>

  <template>
    <div class="modal" v-if="MostrarModal">
      <div class="modal-content">
        <p>¡Bien hecho Jugador {{ ganador }}!</p>
        <button class="modal-content__reset-button" @click="resetGame">Volver a jugar</button>
      </div>
    </div>
  </template>
  
  <style scoped>

Bloque
/* .modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
} */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: rgba(255, 255, 255, 0.8); /* Blanco semitransparente */
  display: flex;
  justify-content: center;
  align-items: center;
}

/* 
.modal-content {
  background-color: #1a1a1d;
  padding: 20px;
  border: 2px solid #c3073f;
  border-radius: 10px;
  width: 80%;
  max-width: 600px;
  max-height: 300px;
  text-align: center;
  text-justify: center;
  color: white;
  font-family: 'Arial', sans-serif;
  animation: fadeIn 0.5s;
} */

.modal-content {
  background-color: #354f52; /* Verde oscuro */
  padding: 30px; /* Aumentado el espaciado interno */
  border: 2px solid #7d0396; /* Color del borde */
  border-radius: 15px; /* Radio del borde */
  width: 90%; /* Ancho */
  /* max-width: 800px; /* Ancho máximo */
  /* max-height: 400px; Altura máxima */ 
  text-align: center;
  color: white; /* Color del texto */
  font-family: 'Arial', sans-serif;
  animation: fadeIn 0.5s;
}
/* Elemento */
/* .modal-content__reset-button {
  background-color: #c3073f;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
} */
.modal-content__reset-button {
  background-color: #a7508d; /* Verde azulado */
  color: white; /* Color del texto del botón */
  padding: 15px 30px; /* Tamaño del botón */
  border: none;
  border-radius: 8px; /* Radio del borde del botón */
  font-size: 18px; /* Tamaño del texto del botón */
  cursor: pointer;
  transition: background-color 0.3s;
}

/* Modificador */
/* .modal-content__reset-button--hover {
  background-color: #ff6f61;
} */
.modal-content__reset-button--hover {
  background-color: #6ab9bf; /* Color del botón al pasar el ratón */
}
/* Animation */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
  </style>