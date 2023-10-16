<template>
    <div>
        <h2>Lista de Notas</h2>
        <div v-if="notas.length === 0" class="sin-notas">No hay notas.</div>
        <div v-else>
            <div v-for="(nota, index) in notas" :key="index" class="nota">
                <h3 class="titulo">{{ nota.titulo }}</h3>
                <p class="contenido">{{ nota.contenido }}</p>
                <button @click="editar(index)" >Editar</button>
                <button @click="eliminar(index)" >Eliminar</button>
            </div>
        </div>
    </div>

    <div class="modal" v-if="show.show">
        <div class="modal-content">
            <h2>Editar Nota</h2>
            <form @submit.prevent="guardar">
                <div>
                    <input v-model="notaEditada.titulo" placeholder="Título" required />
                    <textarea v-model="notaEditada.contenido" placeholder="Contenido" required
                        style="resize: none;"></textarea>
                    <button  type="submit">Guardar</button>
                    <button @click="closeModal">Cancelar</button>
                </div>

            </form>
        </div>
    </div>
</template>

<script setup>
import { defineProps, ref } from 'vue';
import { reactive } from 'vue';

const props = defineProps({
    notas: {
        type: Array,
        default: []
    }
})
let show = reactive({ show: false });
let notaEditada = { titulo: '', contenido: '' };
let id = null;

const emits = defineEmits(['eliminarNota', 'editarNota'])

function editar(index) {
    console.log("Editar nota:", index);
    const infoNota = { ...props.notas[index] };
    notaEditada.titulo = infoNota.titulo;
    notaEditada.contenido = infoNota.contenido;
    id = index;
    show.show = true;
    console.log(show);
}


function eliminar(index) {
    if (confirm('¿Estás seguro de eliminar esta nota?')) {
        emits('eliminarNota', index);
    }
}

function closeModal() {
    show.show = false;
}
function guardar() {
    show.show = false;
    closeModal()
    console.log(id)
    emits('editarNota', id, notaEditada);
    notaEditada = { titulo: '', contenido: '' };

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

button {
    background-color: #0366d6;
    color: #fff;
    padding: 6px 12px;
    border: none;
    cursor: pointer;
    font-weight: 600;
    border-radius: 6px;
    margin-right: 10px;
}

button:hover {
    background-color: #005cbf;
}

.sin-notas {
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

input,
textarea,
button {
    margin-top: 15px;
}

input,
textarea {
    width: 95%;
    padding: 10px;
    border: 1px solid #d1d5da;
    border-radius: 6px;
    background-color: #fff;
    font-size: 16px;
}

input::placeholder,
textarea::placeholder {
    color: #8b949e;
}

input:focus,
textarea:focus {
    border-color: #0366d6;
    box-shadow: 0 0 5px rgba(3, 102, 214, 0.3);
}


</style>
