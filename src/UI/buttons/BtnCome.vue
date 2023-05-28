<template>
  <button class="btn-come"><slot></slot></button>
</template>

<script>
export default {

}
</script>

<style scoped>
.btn-come{
  width: 150px;
  height: 30px;
  background: coral;
  color: whitesmoke;
  border: 2px solid #cb5932;
  margin-top: 30px;
}
</style>