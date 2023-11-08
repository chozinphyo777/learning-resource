<template>
     <ul>
        <learning-resource 
        v-for="res in learningResources" 
        :key="res.id" 
        :title="res.title" 
        :description="res.description" 
        :link="res.link" 
        :id="res.id"
       
       ></learning-resource>
    </ul>
</template>
<script>
import learningResource from './LearningResource.vue';
export default {
    inject:['learningResources'],
    emits : ['deletRes'],
    components :{
        learningResource,
    },
    
}
</script>
<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>