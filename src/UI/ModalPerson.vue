<template>

    <div class="content-dialog">
      <img class="person__photo" :src="stubImg()" alt="">
      <div class="full-info">
        <strong>Name: {{ person.name }} </strong>
        <strong>Alternate Names: {{ person.alternate_names }}</strong>
        <strong>Species: {{ person.species }}</strong>
        <strong>Gender: {{ person.gender }}</strong>
        <strong>House: {{ person.house }}</strong>
        <strong>Date of birth: {{ person.dateOfBirth }}</strong>
        <strong>Wizard: {{ person.wizard }}</strong>
        <strong>Ancestry: {{ person.ancestry }}</strong>
        <strong>Eye Colour: {{ person.eyeColour }}</strong>
        <strong>Hair Colour: {{ person.hairColour }}</strong>
        <div><strong>Wand:</strong>{{ person.wand }}</div>
        <strong>Patronus: {{ person.patronus }}</strong>
        <strong>HogwartsStudent: {{ person.hogwartsStudent }}</strong>
        <strong>HogwartsStaff: {{ person.hogwartsStaff }}</strong>
        <strong>Actor: {{ person.actor }}</strong>
        <strong>Alternate_actors: {{ person.alternate_actors }}</strong>
        <strong>Alive: {{ person.alive }}</strong>
      </div>
      <button @click="$emit('close', false)">Закрыть</button>
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
      if (this.person.image === '') {
        return 'https://ic.pics.livejournal.com/je_nny/14696246/4792536/4792536_2000.jpg'
      } else {
        return this.person.image
      }
    }
  }
}
</script>

<style scoped>
.person__photo {
  width: 300px;
  height: 300px;
}

.full-info {
  display: flex;
  flex-direction: column;
}
.content-dialog{
  background: aqua;
  width: 500px;
}

</style>