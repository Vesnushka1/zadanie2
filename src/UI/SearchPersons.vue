<template>
  <input placeholder="Поиск" @input="sendSearchValue" type="text" name="" id="">
</template>

<script>
export default {
  methods: {
    sendSearchValue(evt) {
      this.$emit('searchValue', evt.target.value)
    }
  }
}
</script>

<style scoped>
input{
  height: 25px;
  outline: none;
  color: #cb5932;
  margin-top: 30px;
}
</style>