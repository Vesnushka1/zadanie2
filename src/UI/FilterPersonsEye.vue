<template>
  <select @change="eyeValue">
    <option value="" selected disabled>Выберите цвет глаз</option>
    <option v-for="eye in filterEye" :key="eye.value">{{eye.value}}</option>
    <option class="opt-default" value="">По умолчанию</option>
  </select>
</template>

<script>
export default {
  props: {
    filterEye: {
      type: Array
    }
  },
  methods:{
    eyeValue(event){
      this.$emit('sendEye', event.target.value)
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