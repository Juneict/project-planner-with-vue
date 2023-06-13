<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNavBar @filter="current=$event"></FilterNavBar>
    <div v-for="project in filterProjects" :key="project.key">
        <single-project :project="project" @delete="deleteProject" @complete="completeProject"/>
    </div>
    {{ current }}
  </div>
</template>

<script>
import FilterNavBar from '../components/FilterNavBar'
import SingleProject from '@/components/SingleProject.vue';

export default {
  name: 'HomeView',
  components: {
    FilterNavBar,
    SingleProject
  },
  data(){
    return{
      projects:[],
      current:"all"
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
  computed:{
    filterProjects(){
      if(this.current === 'completed'){
        return this.projects.filter((project)=>{
            return project.complete
        })
      }
      if(this.current === 'ongoing'){
        return this.projects.filter((project)=>{
          return !project.complete
        })
      }
      return this.projects
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
