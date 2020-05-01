<template>
    <div>
        <h2>Gestion de tareas</h2>

        <span>Vigentes: {{obtenerTareasvigentes}}</span> - <span>Eliminadas: {{contadorEliminadas}} </span> - <span>Totales: {{obtenerTareasTotales}}</span>
        <br><br>
        <tareas-nueva @nuevaTarea="agregarTarea"></tareas-nueva>
        <br>
        <tareas-filtrar v-model="filtro"></tareas-filtrar>

        <div v-if="cargando" class="cargando"><br><br>Cargando... </div>
        <TareasListar v-else  :tareas="obtenerTareasFiltradas" @eliminarTarea="removerTarea"
                      @editarTarea="modificarTarea"/>

        <tareas-notificador :notificar="notificar"></tareas-notificador>
    </div>
</template>

<script>
    import TareasNueva from "./TareasNueva";
    import TareasListar from "./TareasListar";
    import TareasFiltrar from "./TareasFiltrar";
    import TareasNotificador from "./TareasNotificador";

    export default {
        name: 'Tareas',
        components: {TareasListar, TareasNueva, TareasFiltrar, TareasNotificador},
        mounted() {

            //Simulamos request al backend
            this.cargando = true
            setTimeout(()=>{
                this.tareas = ['Aprender Vue', 'Aprender Vuex', 'Aprender Vuetify']
                this.cargando = false
            },1500)
        },
        data() {
            return {
                tareas: [],
                filtro: '',
                contadorEliminadas: 0,
                notificar: null,
                cargando: false
            }
        },
        computed: {
            obtenerTareasFiltradas() {
                let reg = new RegExp(this.filtro, 'i')
                return this.tareas.filter(tarea => reg.test(tarea))
            },
            obtenerTareasvigentes() {
                return this.tareas.length
            },
            obtenerTareasTotales() {
                return this.obtenerTareasvigentes + this.contadorEliminadas
            }
        },
        watch: {
            notificar() {
                setTimeout(() => this.notificar = null, 1500)
            }
        },
        methods: {
            setNotificar(val) {
                this.notificar = val
            },
            agregarTarea(tarea) {
                this.tareas.push(tarea)
                this.setNotificar('agregar')
            },
            removerTarea(index) {
                this.tareas.splice(index, 1)
                this.contadorEliminadas++
                this.setNotificar('eliminar')
            },
            modificarTarea(index, texto) {
                this.$set(this.tareas, index, texto)
                this.setNotificar('editar')
            }
        }
    }
</script>


<style scoped>
    .cargando {
        color: blue
    }
</style>
