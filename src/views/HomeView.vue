<template>
  <div class="home">
      <h1>Home</h1>
      <FilterNav @current="current=$event" :current="current"></FilterNav>
        <div v-for="project in filteredProject" :key="project.id">
            <SingleProject :project="project" @delete="deleteProject" @finish="completeProject"></SingleProject>
        </div>
        
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
// @ is an alias to /src


export default {
  name: 'HomeView',
  data(){
    return{
      projects:[],
      current:"all"
    }
  },
  components: {
    FilterNav,
    SingleProject,
    
  },
  methods:{
    deleteProject(id){
        this.projects=this.projects.filter(project=>{
          return project.id != id
        })
    },
    completeProject(id){
      let findProject=this.projects.find((project)=>{
          return project.id===id
      });
      findProject.complete =!findProject.complete
    }
  },
  computed:{
      filteredProject(){
          if(this.current==='complete'){
            return this.projects.filter((project)=>{
                return project.complete
            })
          }else if(this.current === 'ongoing'){
            return this.projects.filter((project)=>{
              return !project.complete
            })
          }else{
            return this.projects
          }
      }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
        this.projects=datas
    })
    .catch((error)=>{
      console.log(error.message);
    })
  }
}
</script>
