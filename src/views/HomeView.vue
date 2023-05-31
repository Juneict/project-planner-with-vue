<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.key">
        <single-project :project="project" @delete="deleteProject" @complete="completeProject"/>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue';

export default {
  name: 'HomeView',
  components: {
    SingleProject
  },
  data(){
    return{
      projects:[]
    }
  },
  methods:{
    deleteProject(id){
        console.log(id);
        this.projects = this.projects.filter(project=>{
          return project.id != id;
        })
    },
    completeProject(id){
      let findProject = this.projects.find(project=>{
        return project.id=== id;
      })
      findProject.complete = !findProject.complete
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json();
    })
    .then((data)=>{
      this.projects = data
    })
    .catch((err)=>{
      console.log(err.message());
    })
  }
}
</script>
