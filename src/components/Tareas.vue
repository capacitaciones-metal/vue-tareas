<template>
    <div>
        <h2>Gestion de tareas</h2>

        <span>Vigentes: {{obtenerTareasvigentes}}</span> - <span>Eliminadas: {{contadorEliminadas}} </span> - <span>Totales: {{obtenerTareasTotales}}</span>
        <br><br>
        <tareas-nueva ></tareas-nueva>
        <br>
        <tareas-filtrar></tareas-filtrar>

        <div v-if="cargando" class="cargando"><br><br>Cargando... </div>
        <TareasListar v-else />

        <tareas-notificador :notificar="notificar"></tareas-notificador>
    </div>
</template>

<script>
    import {mapActions, mapState, mapMutations} from 'vuex'
    import TareasNueva from "./TareasNueva";
    import TareasListar from "./TareasListar";
    import TareasFiltrar from "./TareasFiltrar";
    import TareasNotificador from "./TareasNotificador";

    export default {
        name: 'Tareas',
        components: {TareasListar, TareasNueva, TareasFiltrar, TareasNotificador},
        mounted() {
           this.cargarTareas()
        },
        computed: {
            ...mapState(['cargando','tareas', 'notificar','contadorEliminadas']), //this.cargando
            obtenerTareasvigentes() {
                return this.tareas.length
            },
            obtenerTareasTotales() {
                return this.obtenerTareasvigentes + this.contadorEliminadas
            }
        },
        watch: {
            notificar() {
                setTimeout(() => this.setNotificar(null), 1500)
            }
        },
        methods: {
            ...mapActions(['cargarTareas']),
            ...mapMutations(['setNotificar'])
        }
    }
</script>


<style scoped>
    .cargando {
        color: blue
    }
</style>
