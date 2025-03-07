<script>
    export default {
        inject: ['recursos','deleteResource'],
    };
</script>

<template>
    <ul>
        <li v-for="element in recursos" :key="element.id">
            <h2>{{ element.titulo }}</h2>
            <p>{{ element.descripcion }}</p>
            <p><a :href="element.url">Ir al enlace</a></p>
            <button @click="deleteResource(element)">Eliminar</button>
            <p>--------------------</p>
        </li>
    </ul>
</template>

<style scoped>
    ul {
        list-style: none;
    }
    h2 {
        color: red;
    }
</style>
