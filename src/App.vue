<template>
  <div>

  </div>
</template>

<script>
export default {
  data(){
    return{
      persons:[]
    }
  },
  methods:{
    async getPersons(){
      let result = await fetch('https://hp-api.onrender.com/api/characters')
      this.persons = await result.json()
    }
  },
  mounted() {
    this.getPersons()
  }
}
</script>

<style scoped>

</style>