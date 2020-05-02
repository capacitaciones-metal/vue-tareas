<template>

    <v-app>
        <v-app-bar app color="primary" dark>
            <v-toolbar-title>Gestion de Tareas</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon target="_blank" href="http://fullstack-extraordinary.com/curso-vue-vuex-vuetify/">
                <v-icon>mdi-link</v-icon>
            </v-btn>
        </v-app-bar>

        <v-content class="grey lighten-3">
            <tareas></tareas>
        </v-content>
    </v-app>

</template>

<script>
    import Tareas from "./components/Tareas";

    export default {
        name: 'App',
        components: {Tareas},
    }
</script>

<style>

</style>
