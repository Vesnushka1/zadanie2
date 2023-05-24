<template>
  <div class="person">
    <img class="person__photo" :src="stubImg()" alt="">
    <div class="person__info">
      <strong>Name: {{ person.name }} </strong>
      <strong>Species: {{ person.species }}</strong>
      <strong>House: {{ person.house }}</strong>
      <strong>Date of birth: {{ person.dateOfBirth }}</strong>
      <strong>Eye Colour: {{ person.eyeColour }}</strong>
      <strong>Gender: {{ person.gender }}</strong>
      <strong>Ancestry: {{ person.ancestry }}</strong>
    </div>
    <button @click.prevent="this.$emit('openDialogValue', true, person)">Смотреть больше</button>
  </div>
</template>

<script>
export default {
  props: {
    person: {
      type: Object
    }
  },
  methods: {
    stubImg() {
      if (this.person.image == '') {
        return 'https://ic.pics.livejournal.com/je_nny/14696246/4792536/4792536_2000.jpg'
      } else {
        return this.person.image
      }
    }
  }
}
</script>

<style scoped>
.person {
  width: 30vw;
  display: flex;
  margin: 10px;
  padding: 10px;
  border: black 1px solid;
}

.person__info {
  display: flex;
  flex-direction: column;
}

.person__photo {
  width: 100px;
  height: 100px;
}
</style>