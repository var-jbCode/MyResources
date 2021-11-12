<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab" />
  </keep-alive>
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';

export default {
  components: {
    AddResource,
    StoredResources,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      resourcesList: [
        {
          id: 'official-guide',
          title: 'Vue Official Guide',
          desc: 'The official Vue.js Docs',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          desc: "The web's top search engine",
          link: 'https://google.com',
        },
      ],
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  provide() {
    return {
      resources: this.resourcesList,
      addResource: this.addResource,
      removeResource: this.removeResource,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, desc, link) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        desc,
        link,
      };
      this.resourcesList.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resID) {
      const resIndex = this.resourcesList.findIndex((res) => res.id === resID);
      this.resourcesList.splice(resIndex, 1);
    },
  },
};
</script>
