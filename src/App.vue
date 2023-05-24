<template>
  <div class="main-block">
    <sorted-persons @selOpt="getSelOpt" :sorted="sorted"/>
    <filter-persons-gender @sendGender="updateValueGender"/>
    <filter-persons-eye :filterEye="filterEye" @sendEye="updateValueEye"/>
    <search-persons @searchValue="getSearchVal"/>
    <person-list @openDialogValue="updateDialogValue" :persons="sortedPersonsEye"/>
    <dialog class="dialogWindow" :open="openDialog">
      <modal-person :person="modelPerson"/>
    </dialog>
  </div>
</template>

<script>
import PersonList from "@/components/PersonList";
import SearchPersons from "@/UI/SearchPersons";
import SortedPersons from "@/UI/SortedPersons";
import FilterPersonsGender from "@/UI/FilterPersonsGender";
import FilterPersonsEye from "@/UI/FilterPersonsEye";
import ModalPerson from "@/UI/ModalPerson";

export default {
  components: {PersonList, SearchPersons, SortedPersons, FilterPersonsGender, FilterPersonsEye, ModalPerson},
  data() {
    return {
      persons: [],
      sorted: [
        {value: 'name', name: 'По возрастанию Name'},
        {value: 'nameReverse', name: 'По убыванию Name'},
        {value: 'house', name: 'По возрастанию House'},
        {value: 'houseReverse', name: 'По убыванию House'},
        {value: 'ancestry', name: 'По возрастанию ancestry'},
        {value: 'ancestryReverse', name: 'По убыванию ancestry'},
      ],
      filterEye: [
        {value: 'green'},
        {value: 'black'},
        {value: 'brown'},
        {value: 'red'},
        {value: 'yellow'},
        {value: 'blue'},
        {value: 'gray'},
        {value: 'white'},
      ],
      selectedValue: '',
      searchValue: '',

      eyeValue: '',
      genderValue: '',
      openDialog: false,
      modelPerson:{}

    }
  },
  methods: {
    async getPersons() {
      let result = await fetch('https://hp-api.onrender.com/api/characters')
      this.persons = await result.json()
    },
    getSelOpt(value) {
      this.selectedValue = value
    },
    getSearchVal(value) {
      this.searchValue = value
    },
    updateValueGender(value) {
      this.genderValue = value
    },
    updateValueEye(value) {
      this.eyeValue = value
    },
    updateDialogValue(value, person){
      this.openDialog= value
      this.modelPerson=person
    }
  },
  computed: {
    sortedPersonsPosts() {
      console.log(this.selectedValue)
      if (this.selectedValue.includes('Reverse')) {
        return [...this.persons].sort((pers1, pers2) => pers1[this.selectedValue.replace('Reverse', '')]?.localeCompare(pers2[this.selectedValue.replace('Reverse', '')])).reverse()
      } else {
        return [...this.persons].sort((pers1, pers2) => pers1[this.selectedValue]?.localeCompare(pers2[this.selectedValue]))
      }
    },
    searchPersonsPosts() {
      return this.sortedPersonsPosts.filter(post => post.name.toLowerCase().includes(this.searchValue.toLowerCase()) || post.ancestry.toLowerCase().includes(this.searchValue.toLowerCase()) || post.house.toLowerCase().includes(this.searchValue.toLowerCase()))
    },
    sortedPersonsGender() {
      if (this.genderValue == '') {
        return this.searchPersonsPosts
      } else {
        return this.searchPersonsPosts.filter(post => post.gender == this.genderValue)
      }
    },
    sortedPersonsEye() {
      if (this.eyeValue == '') {
        return this.sortedPersonsGender
      } else {
        return this.sortedPersonsGender.filter(post => post.eyeColour == this.eyeValue)
      }
    }
  },
  mounted() {
    this.getPersons()
  }
}
</script>

<style scoped>
.main-block {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.dialogWindow{

}
</style>