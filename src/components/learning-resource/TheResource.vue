<template>
  <div id="main">
    <base-card id="tabs">
      <base-btn @click="changeTabs('stored-resources')" :mode="storedResButton"
        >Stored Resources</base-btn
      >
      <base-btn @click="changeTabs('add-resource')" :mode="addResButton"
        >Add Resource</base-btn
      >
    </base-card>

    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';

export default {
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: JSON.parse(localStorage.getItem('storedData')) || [],
    };
  },
  methods: {
    saveData() {
      const parsed = JSON.stringify(this.storedResources);
      localStorage.setItem('storedData', parsed);
    },
    changeTabs(tab) {
      this.selectedTab = tab;
    },
    addResource(title, desc, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: desc,
        link: url,
      };

      this.storedResources.push(newResource);
      this.saveData();
      this.selectedTab = 'stored-resources';
    },
    removeResource(id) {
      const idx = this.storedResources.findIndex((res) => res.id === id);
      this.storedResources.splice(idx, 1);
      this.saveData();
    },
    editResource(id, newTitle, newDesc, newLink) {
      const idx = this.storedResources.findIndex((res) => res.id === id);
      const updatedResource = {
        title: newTitle,
        description: newDesc,
        link: newLink,
      };
      this.storedResources[idx] = updatedResource;
      this.saveData();
      console.log('Done');
    },
  },
  computed: {
    storedResButton() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButton() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  components: {
    AddResource,
    StoredResources,
  },
  watch: {
    storedResources(newValue) {
      localStorage.storedResources = newValue;
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
      editResource: this.editResource,
    };
  },
};
</script>

<style scoped>
</style>