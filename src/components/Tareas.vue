<template>
    <v-container>
        <v-row>
            <v-col cols="8">
                <v-card>
                    <v-card-text>
                        <tareas-nueva></tareas-nueva>
                    </v-card-text>
                </v-card>



                <v-card class="mt-3" >
                    <v-card-text>
                        <div v-if="cargando" class="cargando"><br><br>Cargando...</div>
                        <TareasListar v-else/>
                    </v-card-text>
                </v-card>
            </v-col>

            <v-col cols="4">

                <v-card >
                    <v-card-text>
                        <tareas-filtrar></tareas-filtrar>
                    </v-card-text>
                </v-card>

                <v-card class="mt-3">
                    <v-card-text>
                        <span>Vigentes: {{obtenerTareasvigentes}}</span> -
                        <span>Eliminadas: {{contadorEliminadas}} </span> -
                        <span>Totales: {{obtenerTareasTotales}}</span>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>


        <tareas-notificador :notificar="notificar"></tareas-notificador>
    </v-container>

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
            ...mapState(['cargando', 'tareas', 'notificar', 'contadorEliminadas']), //this.cargando
            obtenerTareasvigentes() {
                return this.tareas.length
            },
            obtenerTareasTotales() {
                return this.obtenerTareasvigentes + this.contadorEliminadas
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
