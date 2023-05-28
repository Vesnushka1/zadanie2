<template>
  <div class="content-dialog">
    <img class="person__photo" :src="stubImg()" alt="" />
    <div class="full-info">
      <div class="info-name">{{ person.name }}</div>
      <div class="info">
        <strong>Alternate Names: </strong>{{ person.alternate_names }}
      </div>
      <div class="info"><strong>Species: </strong>{{ person.species }}</div>
      <div class="info"><strong>Gender: </strong>{{ person.gender }}</div>
      <div class="info"><strong>House: </strong>{{ person.house }}</div>
      <div class="info">
        <strong>Date of birth: </strong>{{ person.dateOfBirth }}
      </div>
      <div class="info"><strong>Wizard: </strong>{{ person.wizard }}</div>
      <div class="info"><strong>Ancestry: </strong>{{ person.ancestry }}</div>
      <div class="info">
        <strong>Eye Colour: </strong>{{ person.eyeColour }}
      </div>
      <div class="info">
        <strong>Hair Colour: </strong>{{ person.hairColour }}
      </div>
      <div class="info">
        <strong>Wand: </strong> {{ person.wand.wood }}, {{ person.wand.core }},
        {{ person.wand.length }}
      </div>
      <div class="info"><strong>Patronus: </strong>{{ person.patronus }}</div>
      <div class="info">
        <strong>HogwartsStudent: </strong>{{ person.hogwartsStudent }}
      </div>
      <div class="info">
        <strong>HogwartsStaff: </strong>{{ person.hogwartsStaff }}
      </div>
      <div class="info"><strong>Actor: </strong>{{ person.actor }}</div>
      <div class="info">
        <strong>Alternate_actors: </strong>{{ person.alternate_actors }}
      </div>
      <div class="info"><strong>Alive: </strong>{{ person.alive }}</div>
    </div>
    <BtnClose class="btn-close" @click="$emit('close', false)">X</BtnClose>
  </div>
</template>

<script>
import BtnClose from "@/UI/buttons/BtnClose.vue";

export default {
  components: {BtnClose},
  props: {
    person: {
      type: Object,
    },
  },
  methods: {
    stubImg() {
      if (this.person.image === "") {
        return "https://ic.pics.livejournal.com/je_nny/14696246/4792536/4792536_2000.jpg";
      } else {
        return this.person.image;
      }
    },
  },
};
</script>

<style scoped>
.person__photo {
  width: 250px;
  height: 270px;
  margin-right: 20px;
}

.info-name {
  color: coral;
  font-size: 26px;
}

.full-info {
  display: flex;
  flex-direction: column;
}

.content-dialog {
  background: #ffffff;
  width: 600px;
  display: flex;
  position: relative;
  padding: 20px;
  box-shadow: #cb5932 7px 7px 10px 7px;
  margin-top: 150px;
}

</style>
