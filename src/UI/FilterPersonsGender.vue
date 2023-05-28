<template>
  <select @change="genderValue">
    <option value="" selected disabled>Выберите пол</option>
    <option value="male">Мужчина</option>
    <option value="female">Женщина</option>
    <option class="opt-default" value="">По умолчанию</option>
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
select{
  margin-top: 10px;
}
select option{
  background: coral;
  color: white;
}
.opt-default {
  background: #ffa17e;
  color: white;
}
</style>