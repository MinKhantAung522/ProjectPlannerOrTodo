<template>
  <nav>
      <small @click="filternav('all')" :class="{active : current ==='all'}">all</small>
      <small @click="filternav('complete')" :class="{active : current === 'complete'}">complete</small>
      <small @click="filternav('ongoing')" :class="{active : current === 'ongoing'}">ongoing</small>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods:{
        filternav(value){
            this.$emit('filterValue',value);
        }
    }
}
</script>

<style scoped>
small{
    margin-right: 15px;
    font-weight: bold;
    cursor: pointer;
    color: grey;
}
.active{
    color: darkred;
}

</style>