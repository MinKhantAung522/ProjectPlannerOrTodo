<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="updateProject">
      <label>PROJECT NAME</label>
      <input type="text" v-model="name">
      <label>PROJECT DETAILS</label>
      <input type="text" v-model="detail">
      <div class="form-button">
          <button type="submit">Update Project</button>
      </div>
  </form>
</template>

<script>
export default {
props:['id'],
data(){
    return{
        name:'',
        title:''
    }
},
mounted(){
    fetch('http://localhost:3000/project/' + this.id)
    .then((res)=>{
        return res.json();
    })
    .then((data)=>{
        this.name = data.name;
        this.detail = data.detail;
    })
    .catch((err)=>{
        console.log(err);
    })
},
methods:{
    updateProject(){
        fetch('http://localhost:3000/project/' + this.id,{
            method:'PATCH',
            headers:{
                "Content-Type":"application/json"
            },
            body:JSON.stringify(
                {
                    name:this.name,
                    detail:this.detail
                }
            )
        })
        .then(()=>{
            this.$router.push('/')
        })
        .catch((err)=>{
            console.log(err);
        })

    }
}
}
</script>

<style>

</style>