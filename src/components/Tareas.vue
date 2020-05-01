<template>
    <div>
        <h2>Gestion de tareas</h2>

        <tareas-nueva  @nuevaTarea="agregarTarea" ></tareas-nueva>

        <TareasListar :tareas="tareas" @eliminarTarea="removerTarea" @editarTarea="modificarTarea" />

    </div>
</template>

<script>
    import TareasNueva from "./TareasNueva";
    import TareasListar from "./TareasListar";

    export default {
        name: 'Tareas',
        components: {TareasListar, TareasNueva},
        data(){
            return {
                tareas: ['Aprender Vue', 'Aprender Vuex', 'Aprender Vuetify']
            }
        },
        methods:{
            agregarTarea(tarea){
                this.tareas.push(tarea)
            },
            removerTarea(index){
                this.tareas.splice(index,1)
            },
            modificarTarea(index,texto){
                this.$set(this.tareas,index,texto)
            }
        }
    }
</script>


