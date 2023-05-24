<template>
  <div class="main-block">
    <sorted-persons/>
    <search-persons/>
    <person-list :persons="persons"/>
  </div>
</template>

<script>
import PersonList from "@/components/PersonList";
import SearchPersons from "@/UI/SearchPersons";
import SortedPersons from "@/UI/SortedPersons";
export default {
  components: {PersonList, SearchPersons,SortedPersons},
  data(){
    return{
      persons:[],
      sorted:[
        {value:'name', name: 'По возрастанию Name'},
        {value:'nameReverse', name: 'По убыванию Name'},
        {value:'house', name: 'По возрастанию House'},
        {value:'houseReverse', name: 'По убыванию House'},
        {value:'ancestry', name: 'По возрастанию ancestry'},
        {value:'ancestryReverse', name: 'По убыванию ancestry'},
      ]
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
.main-block{
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>