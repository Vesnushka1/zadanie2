<template>
<select @change="sendSelectedOption">
  <option disabled selected>Выберите значение</option>
  <option v-for="option in sorted" :value="option.value" :key="option.name"> {{option.name}}</option>
  <option>По умолчанию</option>
</select>
</template>

<script>
export default {
  props:{
    sorted:{
      type:Array,
      default: ()=>[]
    }
  },
  methods:{
    sendSelectedOption(evt){
      this.$emit('selOpt', evt.target.value)
    }
  }
}
</script>

<style scoped>

</style>