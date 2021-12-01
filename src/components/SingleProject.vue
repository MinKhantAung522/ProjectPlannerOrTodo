<template>
  <div class="project" :class="{complete: project.complete}">
    <div class="flexing">
      <div>
        <h3 @click="showDetail">Name -- {{ project.name }}</h3>
      </div>
      <div>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons" @click="update"> edit </span>
        <span class="material-icons" @click="completeProject"> done </span>
      </div>
    </div>
    <p v-if="this.show">Detail -- {{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      show: false,
      api: "http://localhost:3000/project/"
    };
  },
  methods: {
    showDetail() {
      this.show = !this.show;
    },
    deleteProject(){
      let deleteItem = this.api + this.project.id;
      fetch(deleteItem,{method:"DELETE"})
      .then(()=>{
        this.$emit("delete",this.project.id);
      })
      .catch((err)=>{
        console.log(err);
      })
    },
    completeProject(){
      let completeItem = this.api + this.project.id;
      fetch(completeItem,{
        method:"PATCH",
        headers:{
          "Content-Type": 'application/json'
        },
        body:JSON.stringify(
          {
            complete: !this.project.complete
          }
        )
      })
      .then(()=>{
        this.$emit("complete",this.project.id);
      })
      .catch((err)=>{
        console.log(err);
      })
    },
    update(){
      this.$router.push('/editProject/'+ this.project.id)
    }

    
  },
};
</script>

<style scoped>
.project {
  margin-bottom: 15px;
  padding: 15px;
  padding-left: 20px;
  background: wheat;
  border-left: crimson solid 20px;
  border-radius: 9px;
}
h3 {
  color: indigo;
  cursor: pointer;
}
.flexing{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
span{
    margin-left: 10px;
    cursor: pointer;
}
span:hover{
  color: indigo;
}
.complete{
  border-left-color: green;
}
</style>