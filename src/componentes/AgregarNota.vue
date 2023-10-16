<template>
  <div>
    <h2>Agregar Nueva Nota</h2>
    <form @submit.prevent="agregar(this)" class="form">
      <input v-model="nuevaNota.titulo" class="input" placeholder="Título" required />
      <textarea v-model="nuevaNota.contenido" class="textarea" placeholder="Contenido" required style="resize: none;"></textarea>
      <button type="submit" class="button">Guardar Nota</button>
    </form>
  </div>
</template>
  
<script setup>
import { reactive } from 'vue';

let nuevaNota = reactive({ titulo: '', contenido: '' })

function agregar(cntx) {
  cntx.$emit('nuevaNota', { ...nuevaNota });
  nuevaNota.titulo = '';
  nuevaNota.contenido = '';
}

</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
}

.input,
.textarea,
.button {
  margin-top: 15px;
}

.input,
.textarea {
  width: 30vw;
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
  padding: 10px;
  border: none;
  cursor: pointer;
  font-weight: 600;
  border-radius: 6px;
  text-align: center;
}

.button:hover {
  background-color: #005cbf;
}
</style>
  