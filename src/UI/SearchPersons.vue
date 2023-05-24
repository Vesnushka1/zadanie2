<template>
  <input @input="sendSearchValue" type="text" name="" id="">
</template>

<script>
export default {
  methods:{
    sendSearchValue(evt){
      this.$emit('searchValue', evt.target.value)
    }
  }
}
</script>

<style scoped>

</style>