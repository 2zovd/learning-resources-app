<template>
  <div>
    <base-card>
      <base-button
        @click.prevent="setSelectedTab('stored-resources')"
        :mode="storedResButtonMode"
      >Stored Resource</base-button>
      <base-button
        @click.prevent="setSelectedTab('add-resource')"
        :mode="addResButtonMode"
      >Add Resource</base-button>
    </base-card>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      title: 'Resources App',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official guide',
          description: 'The only official Vue.js documentation.',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Find it here',
          link: 'https://vuejs.org'
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    }
  }
};
</script>