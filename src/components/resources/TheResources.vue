<template>
    <base-card>
        <base-button
        @click="setSelectedTab('stored-resources')"
        :mode="storedResButtonMode" >
            Stored Resources
        </base-button>
        <base-button
        @click="setSelectedTab('add-resource')"
        :mode="addResButtonMode" >
        Add Resource
    </base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
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
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learning to Google...',
                    link: 'https://google.com'
                }
            ]
        };
    },

    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.deleteResource
        }
    },

    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resources' ? null : 'flat';
        }
    },

    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, link) {
            const newResource = {
                id: new Date().toISOString(),
                title,
                description,
                link
            }

            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        deleteResource(id) {
            const index = this.storedResources.findIndex(res => res.id === id);
            this.storedResources.splice(index, 1);
        }
    }
}
</script>import { toISOString } from 'core-js/core/date';import { push } from 'core-js/core/array';
./StoredResources.vueimport { unshift } from 'core-js/core/array';

