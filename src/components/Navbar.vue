<template>
  <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/addProject">Add Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style scoped>
    nav{
        text-align: center;
    }
    nav a{
        text-decoration: none;
        margin: 5px;
        font-size: 25px;
        padding: 20px;
    }
    a.router-link-active{
        border-bottom: 5px darkred solid;

    }
</style>
