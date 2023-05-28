<template>
  <div class="person">
    <img class="person__photo" :src="stubImg()" alt="" />
    <div class="person__info">
      <div class="info-name">{{ person.name }}</div>
      <div class="info"><strong>Species: </strong>{{ person.species }}</div>
      <div class="info"><strong>House: </strong>{{ person.house }}</div>
      <div class="info">
        <strong>Date Of Birth: </strong>{{ person.dateOfBirth }}
      </div>
      <div class="info">
        <strong>Eye Colour: </strong>{{ person.eyeColour }}
      </div>
      <div class="info"><strong>Gender: </strong>{{ person.gender }}</div>
      <div class="info"><strong>Ancestry: </strong>{{ person.ancestry }}</div>
    </div>
    <button
      class="btn-more"
      @click.prevent="this.$emit('openDialogValue', true, person)"
    >
      More...
    </button>
    <button
      v-if="successfulAuth"
      @click.prevent="favouritePerson"
      class="btn-favour"
    >
      Добавить в избранное
    </button>
  </div>
</template>

<script>
export default {
  props: {
    person: {
      type: Object,
    },
    successfulAuth: {
      type: Boolean,
    },
  },
  data() {
    return {
      fav: false,
    };
  },
  methods: {
    stubImg() {
      if (this.person.image === "") {
        return "https://ic.pics.livejournal.com/je_nny/14696246/4792536/4792536_2000.jpg";
      } else {
        return this.person.image;
      }
    },
    favouritePerson(event) {
      if (this.fav === false) {
        event.target.textContent = "Удалить из избранного";
        event.target.classList.add("btn-favour-active");
        this.fav = true;
        this.$emit("favPerson", this.person);
        console.log(this.person);
      } else {
        event.target.textContent = "Добавить в избранное";
        event.target.classList.remove("btn-favour-active");
        this.$emit("favPersonDel", this.person);
        this.fav = false;
      }
    },
  },
};
</script>

<style scoped>
.person {
  width: 600px;
  display: flex;
  margin: 30px;
  position: relative;
}

.person__info {
  display: flex;
  flex-direction: column;
}

.person__photo {
  width: 110px;
  height: 140px;
  border: coral 5px solid;
  margin-right: 20px;
}

.info-name {
  font-size: 32px;
}

.btn-more {
  width: 70px;
  height: 20px;
  align-self: end;
  background: coral;
  color: whitesmoke;
  border: 2px solid #cb5932;
  position: absolute;
  right: 180px;
}

.btn-favour {
  width: 150px;
  height: 40px;
  align-self: end;
  background: coral;
  color: whitesmoke;
  border: 2px solid #cb5932;
  position: absolute;
  right: 0px;
}

.btn-favour-active {
  background: #ff4700;
  color: whitesmoke;
  border: 2px solid #cb5932;
}
</style>
