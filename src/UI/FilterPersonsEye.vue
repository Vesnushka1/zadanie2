<template>
  <select @change="eyeValue">
    <option value="" selected>По умолчанию</option>
    <option v-for="eye in filterEye" :key="eye.value">{{eye.value}}</option>
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

</style>