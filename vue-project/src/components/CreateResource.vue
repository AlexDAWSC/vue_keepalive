<script>
    import Error from './Error.vue';
    export default {
        inject: ['recursos','addResource','toggleComponent','changeError','error'],
        components: {
            Error,
        },
        data() {
            return {
                id: this.recursos.length,
                titulo: "",
                descripcion: "",
                url: "",
            };
        },
        methods: {
            comprobar() {
                if (this.titulo==="" || this.descripcion==="" || this.url==="") {
                    this.changeError(true);
                } else {
                    this.addResource({id: this.id, titulo: this.titulo, descripcion: this.descripcion, url: this.url});
                    this.titulo = "";
                    this.descripcion = "";
                    this.url = "";
                    this.changeError(false);
                    this.toggleComponent('ResourceList');
                }
            } 
        },
    };
</script>

<template>
    <teleport to='body'>
        <Error v-show="error"/>
    </teleport>
    <form @submit.prevent="comprobar">
        <p><input type="text" v-model="titulo" placeholder="Titulo"></p>
        <p><textarea v-model="descripcion" placeholder="Descripcion"></textarea></p>
        <p><input type="url" v-model="url" placeholder="URL"></p>
        <button type="submit">Add</button>
    </form>
</template>