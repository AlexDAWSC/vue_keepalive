<script>
  import ResourceList from './components/ResourceList.vue';
  import CreateResource from './components/CreateResource.vue';
import { KeepAlive } from 'vue';
import { computed } from 'vue';
  export default{
    components: {
    ResourceList,
    CreateResource
    },
    provide() {
      return {
        recursos: this.lista,
        addResource: this.addResource,
        toggleComponent: this.toggleComponent,
        deleteResource: this.deleteResource,
        changeError: this.changeError,
        error: computed(() => this.changeError),
      }
    },
    data() {
      return {
        tabs: ['ResourceList','CreateResource'],
        recursos: [],
        currentTab: "ResourceList",
        error: false,
      };
    },
    methods: {
      addResource(resource) {
        this.recursos.push({id: resource.id, titulo: resource.titulo, descripcion: resource.descripcion, url: resource.url});
      },
      toggleComponent(cadena) {
        this.currentTab = cadena;
        if (cadena==="ResourceList") {
          this.error = false;
        }
      },
      deleteResource(resource) {
        const index = this.recursos.findIndex(element => element===resource);
        this.recursos.splice(index,1);
      },
      changeError(bool) {
        this.error = bool;
      }
    },
    computed: {
      lista() {
        return this.recursos;
      },
      errorComp() {
        return this.error;
      }
    }
  };
</script>

<template>
  <div>
    <button @click="toggleComponent('ResourceList')">Ver lista</button>
    <button @click="toggleComponent('CreateResource')">Anadir elemento</button>
    <KeepAlive include="CreateResource">
      <component :is="currentTab"></component>
    </KeepAlive>
  </div>
</template>

<style scoped>
  div {
    border: 1px solid red;
    width: 600px;
    margin-left: 50%;
    margin-right: 50%;
  }
</style>