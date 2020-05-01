<template>
    <ul>
        <li v-for="(tarea,index) in tareas" :key="index">

            <template v-if="editando === index">
                <input type="text" v-model="texto" @keyup.enter="emitirTareaEditada" />
                <button @click="emitirTareaEditada">confirmar</button>
            </template>

            <template v-else>
                {{tarea}}
                <button class="editar" @click="editarTarea(index,tarea)">editar</button>
                <button class="eliminar" @click="$emit('eliminarTarea',index)">eliminar</button>
            </template>


        </li>
    </ul>
</template>

<script>
    export default {
        name: 'TareasListar',
        props: {
            tareas: {}
        },
        data(){
            return {
                editando: null,
                texto: ''
            }
        },
        methods:{
            editarTarea(index,tarea){
                this.editando = index
                this.texto = tarea
            },
            emitirTareaEditada(){
                this.$emit('editarTarea', this.editando, this.texto)
                this.editando = null
                this.texto = ''
            }
        }
    }
</script>

<style>
    .eliminar {
        border: none;
        background-color: transparent;
        color: red
    }

    .editar {
        border: none;
        background-color: transparent;
        color: blue
    }

</style>
