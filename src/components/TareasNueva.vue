<template>
    <div>
        <label>Nueva Tarea: </label>
        <input type="text" v-model="tarea" @keyup.enter="agregarTarea" />
        <button @click="agregarTarea">Agrear</button>
    </div>
</template>

<script>
    export default {
        name: "TareasNueva",
        data(){
            return {
                tarea:''
            }
        },
        methods:{
            agregarTarea(){
                if(this.tarea.length > 0){
                    this.$emit('nuevaTarea',this.tarea)
                    this.tarea = ''
                }else{
                    alert('La tarea no puede estar vacia')
                }
            }
        }
    }
</script>

<style scoped>

</style>
