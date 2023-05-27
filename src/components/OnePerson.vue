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
    <button v-if="successfulAuth" @click.prevent="favouritePerson" class="btn-favour">Добавить в избранное</button>
  </div>
</template>

<script>
export default {
  props: {
    person: {
      type: Object
    },
    successfulAuth: {
      type: Boolean
    }
  },
  data() {
    return {
      fav: false
    }
  },
  methods: {
    stubImg() {
      if (this.person.image === '') {
        return 'https://ic.pics.livejournal.com/je_nny/14696246/4792536/4792536_2000.jpg'
      } else {
        return this.person.image
      }
    },
    favouritePerson(event) {
      if (this.fav === false) {
        event.target.textContent = 'Удалить из избранного'
        this.fav = true
        this.$emit('favPerson', this.person)
        console.log(this.person)
      } else {
        event.target.textContent = 'Добавить в избранное'
        this.$emit('favPersonDel', this.person)
        this.fav = false
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