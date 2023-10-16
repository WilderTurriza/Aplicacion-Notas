<template>
    <div>
        <h2>Lista de Notas</h2>
        <div v-if="notas.length === 0" class="no-notes">No hay notas.</div>
        <div v-else>
            <div v-for="(nota, index) in notas" :key="index" class="nota">
                <h3 class="titulo">{{ nota.titulo }}</h3>
                <p class="contenido">{{ nota.contenido }}</p>
                <button @click="editar(index)" class="button">Editar</button>
                <button @click="eliminar(index)" class="button">Eliminar</button>
            </div>
        </div>
    </div>

    <EditarNota :show="showModal" :title="titulo" :note="contenido" :id="id_nota" @cerrar="cerrarDialog" @guardar="guardarInfo"></EditarNota>

</template>

<script setup>
import { defineProps } from 'vue';
import EditarNota from './EditarNota.vue';

const props = defineProps({
    notas: {
        type: Array,
        default: []
    }
})
let showModal = false;
let titulo = "";
let contenido = "";
let id_nota = null;

const emits = defineEmits(['eliminarNota', 'editarNota'])

function editar(index) {
    console.log("Editar nota:", index);
    const infoNota = { ...props.notas[index] };
    titulo = infoNota.titulo;
    contenido = infoNota.contenido;
    id_nota = index; 
    showModal = true; 
    console.log("show:", showModal);
    console.log("titulo:", titulo);
    console.log("contenido:", contenido);

}


function eliminar(index) {
    if (confirm('¿Estás seguro de eliminar esta nota?')) {
        emits('eliminarNota', index);
    }
}

function cerrarDialog() {
    showModal = false;
    console.log(showModal)
}
function guardarInfo(id,notaEditada) {
    console.log(notaEditada)
    emits('editarNota', id, notaEditada);
    showModal = false;

}
</script>
  
<style scoped>
.nota {
    background-color: #fff;
    border: 1px solid #e1e4e8;
    border-radius: 6px;
    padding: 16px;
    margin: 10px 0;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.titulo {
    font-size: 20px;
    font-weight: 600;
    margin-top: 0;
    color: #333;
}

.contenido {
    font-size: 16px;
    color: #555;
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

.no-notes {
    color: #777;
    font-size: 18px;
}



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
</style>