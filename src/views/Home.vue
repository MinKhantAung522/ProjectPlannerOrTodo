<template>
  <div class="home">
    <h1>Home</h1>
    <FilterNav @filterValue = "current =$event" :current ="current" class="filter"></FilterNav>
    <div v-for="project in filterProjects" :key="project.id">
      <SingleProject :project="project" @delete="deletee" @complete="completeItem"></SingleProject>
    </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
// @ is an alias to /src

export default {
  name: 'Home',
  data(){
    return{
      projects:[],
      current:'all'
    }
  },
  components: {
    FilterNav,
    SingleProject,
    
  },
  methods:{
    deletee(id){
      this.projects = this.projects.filter(project=>{
        return project.id != id;
      })
    },
    completeItem(id){
      let completeItem = this.projects.find(project=>{
        return project.id == id;
      })
      completeItem.complete = !completeItem.complete; 
    }
  },
  computed:{
    filterProjects(){
      if(this.current ==="complete"){
        return this.projects.filter((project)=>{
          return project.complete;
        })
      }else if(this.current === "ongoing"){
        return this.projects.filter((project)=>{
          return !project.complete;
        })
      }
      return this.projects;
    }
  },
  mounted(){
    fetch("http://localhost:3000/project")
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
      this.projects = datas;
    })
    .catch((err)=>{
      console.log(err.message);
    })
  }
}
</script>
<style scoped>
.filter{
  margin-bottom: 10px;
}
</style>
