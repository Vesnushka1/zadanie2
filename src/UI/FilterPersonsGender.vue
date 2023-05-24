<template>
  <select @change="genderValue">
    <option value="" selected>По умолчанию</option>
    <option value="male">Мужчина</option>
    <option value="female">Женщина</option>
  </select>

</template>

<script>
export default {
  methods:{
    genderValue(event){
      this.$emit('sendGender', event.target.value)
    }
  }
}
</script>

<style scoped>

</style>