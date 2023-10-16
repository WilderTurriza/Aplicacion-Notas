<template>
  <div class="modal" v-if="show">
    <div class="modal-content">
      <h2>Editar Nota</h2>
      <div>
        <input v-model="notaEditada.titulo" class="input" placeholder="Título" required />
        <textarea v-model="notaEditada.contenido" class="textarea" placeholder="Contenido" required
          style="resize: none;"></textarea>
      </div>
      <button @click="guardar" class="button">Guardar</button>
      <button @click="cerrar" class="button">Cancelar</button>
    </div>
  </div>
</template>
    
<script setup>
import { reactive } from 'vue';
const props = defineProps({
  show: {
    type: Boolean,
    default: false
  },
  title: {
    type: String,
    default: ""
  },
  note: {
    type: String,
    default: ""
  },
  id: {
    type: Number,
    default: null
  },
})


let notaEditada = reactive({ titulo: props.title, contenido: props.note });

const emits = defineEmits(['cerrarDialog', 'guardarInfo']);

function guardar() {
  console.log(notaEditada)
  console.log(props.id)
  emits('guardarInfo', props.id, notaEditada);
  cerrar();
}

function cerrar() {
  emits('cerrarDialog');
}
</script>
  
<style scoped>
.modal {
  position: absolute;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0);
  border-radius: 3rem;
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 100%;
  border-radius: 0.2rem;
}

.input,
.textarea,
.button {
  margin-top: 15px;
}

.input,
.textarea {
  width: 95%;
  padding: 10px;
  border: 1px solid #d1d5da;
  border-radius: 6px;
  background-color: #fff;
  font-size: 16px;
}

.input::placeholder,
.textarea::placeholder {
  color: #8b949e;
}

.input:focus,
.textarea:focus {
  border-color: #0366d6;
  box-shadow: 0 0 5px rgba(3, 102, 214, 0.3);
}

.button {
  background-color: #0366d6;
  color: #fff;
  padding: 6px 12px;
  border: none;
  cursor: pointer;
  font-weight: 600;
  border-radius: 6px;
  margin-right: 10px;
}

.button:hover {
  background-color: #005cbf;
}
</style>
    