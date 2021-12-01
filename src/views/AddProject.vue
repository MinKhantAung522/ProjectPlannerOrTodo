<template>
  <h1>Add Project</h1>
  <form @submit.prevent="addProject">
      <label>PROJECT NAME</label>
      <input type="text" v-model="name">
      <label>PROJECT DETAILS</label>
      <input type="text" v-model="detail">
      <div class="form-button">
          <button type="submit">Add Project</button>
      </div>
  </form>
</template>

<script>
export default {
    data(){
        return{
            name:'',
            detail:''
        }
    },
    methods:{
        addProject(){
            fetch('http://localhost:3000/project',{
                method:'POST',
                headers:{
                    'Content-Type':'application/json'
                },
                body:JSON.stringify(
                    {
                        name:this.name,
                        detail:this.detail,
                        complete:false
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
    form{
        background: wheat;
        border-radius: 20px;
        border: 2px  solid darkred;
    }
    label{
        display: block;
        
        padding: 20px;
    }
    input{
        
        width: 90%;
        height: 30px;
        border: none;
        border-bottom: 1px solid black;
        background: wheat;
        margin-left: 25px;        
        margin-bottom: 20px;
        margin-top: -15px;
    }
    input:focus{
        background: wheat;
        border: none;
        border-bottom: 1px solid black;
    }
    button{
        padding: 14px;
        border-radius: 20px;
        border: darkred 2px solid;
        background: darkred;
        color: wheat;
    }
    button:hover{
        background: rgb(240, 83, 83);
        color: black;
    }
    .form-button{
        margin-bottom: 20px;
        padding: 40px;
        text-align: center;
    }

</style>