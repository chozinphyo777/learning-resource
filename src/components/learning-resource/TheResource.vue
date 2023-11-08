<template>
    <base-card>
        <base-button
         @click="SelectTab('stored-resource')" 
         :mode="StoredResourceMode"
         >Stored Resources
         </base-button>

        <base-button 
        @click="SelectTab('add-resource')" 
        :mode="AddResourceMode"
        >Add Resource
        </base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>
<script>
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';
export default {
     components : {
        StoredResource,
        AddResource,
    },
    data(){
        return {
            selectedTab : 'stored-resource',
            storedResources : [
            {
                id : 'vue-course',
                title : 'Vue',
                description : 'Hello Vue',
                link : 'https://vuejs.org',
            },
            {
                id : 'google-learning',
                title : 'Google',
                description : 'Hello Google',
                link : 'https://google.com',
            }
        ]
        }
    },
    computed:{
        StoredResourceMode(){
            return this.selectedTab === 'stored-resource' ? null : 'flat';
        },
        AddResourceMode(){
            return this.selectedTab === 'add-resource' ? null : 'flat';
        },
    },
   
    provide(){
        return{
            learningResources : this.storedResources,
            addRes : this.addResource,
            deletRes : this.deleteResource,
        }
    },
    methods:{
        SelectTab(tab){
            this.selectedTab = tab;
        },
        addResource(title,des,link){
            const data = {
                id : new Date().toISOString(),
                title : title,
                description : des,
                link : link,
            }
            this.storedResources.unshift(data);
            this.selectedTab = 'stored-resource';
        },
        deleteResource(id){
            //provide and inject doesn't update storedResource
            // this.StoredResource = this.storedResources.filter(res => res.id !== id)
            //  console.log(this.StoredResource);
             const resIndex = this.storedResources.findIndex(res => res.id == id)
             this.storedResources.splice(resIndex,1)

        }
       
    }
    
}
</script>
<style scoped>

</style>