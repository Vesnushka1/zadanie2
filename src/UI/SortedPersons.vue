<template>
<select>
  <option disabled selected>Выберите значение</option>
  <option v-for="option in sorted"> {{option.name}}</option>
</select>
</template>

<script>
export default {
  name: "SortedPersons",
  props:{
    sorted:{
      type:Array
    }
  }
}
</script>

<style scoped>

</style>