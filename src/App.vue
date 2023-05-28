<template>
  <div class="main-block">
    <header class="main-block__header">
      <button class="btn-reg" @click.prevent="openDialogReg = true">
        Регистрация
      </button>
      <button class="btn-reg" @click.prevent="openDialogAuth = true">
        Авторизация
      </button>
      <div class="info-user" v-if="successfulAuth">
        {{ modelUser.name }}
        {{ modelUser.fam }}
        {{ modelUser.otch }}
      </div>
    </header>

    <div class="filters">
      <p>Сортировка</p>
      <sorted-persons @selOpt="getSelOpt" :sorted="sorted"/>
      <filter-persons-gender @sendGender="updateValueGender"/>
      <filter-persons-eye :filterEye="filterEye" @sendEye="updateValueEye"/>
      <search-persons @searchValue="getSearchVal"/>
    </div>

    <div class="favourites">
      <p>Волшебники: {{ favouriteWiz.length }}</p>
      <p>Не волшебники: {{ favouriteNoWiz.length }}</p>
    </div>

    <person-list
        :successfulAuth="successfulAuth"
        @favPerson="favourPerson"
        @favPersonDel="favourPersonDel"
        @openDialogValue="updateDialogValue"
        :persons="sortedPersonsEye"
    />

    <!-- модальное окно подобнее о персонаже -->
    <div @click="openDialog = false" class="dialogWindow" v-if="openDialog">
      <modal-person @click.stop @close="closeModal" :person="modelPerson"/>
    </div>

    <!-- модальное окно регистрации -->
    <dialog :open="openDialogReg" class="dialogRegistration">
      <RegistrationWindow
          @closeRegAfterReg="openDialogReg = false"
          @keydown.esc="openDialogReg = false"
          @closeReg="(val) => (openDialogReg = val)"
      />
    </dialog>

    <!-- модальное окно авторизации -->
    <dialog :open="openDialogAuth" class="dialogAuth">
      <AuthWindow
          @sendUser="successAuth"
          @closeAuthWind="(value) => (openDialogAuth = value)"
          @succesAuth="(val2) => (successfulAuth = val2)"
          @closeAuth="(val1) => (openDialogAuth = val1)"
      />
    </dialog>
  </div>
</template>

<script>
import PersonList from "@/components/PersonList";
import SearchPersons from "@/UI/SearchPersons";
import SortedPersons from "@/UI/SortedPersons";
import FilterPersonsGender from "@/UI/FilterPersonsGender";
import FilterPersonsEye from "@/UI/FilterPersonsEye";
import ModalPerson from "@/UI/ModalPerson";
import RegistrationWindow from "@/UI/RegistrationWindow";
import AuthWindow from "@/UI/AuthWindow";

export default {
  components: {
    AuthWindow,
    PersonList,
    SearchPersons,
    SortedPersons,
    FilterPersonsGender,
    FilterPersonsEye,
    ModalPerson,
    RegistrationWindow,
  },
  data() {
    return {
      persons: [],
      sorted: [
        {value: "name", name: "По возрастанию Name"},
        {value: "nameReverse", name: "По убыванию Name"},
        {value: "house", name: "По возрастанию House"},
        {value: "houseReverse", name: "По убыванию House"},
        {value: "ancestry", name: "По возрастанию ancestry"},
        {value: "ancestryReverse", name: "По убыванию ancestry"},
      ],
      filterEye: [
        {value: "green"},
        {value: "black"},
        {value: "brown"},
        {value: "red"},
        {value: "yellow"},
        {value: "blue"},
        {value: "gray"},
        {value: "white"},
      ],
      selectedValue: "",
      searchValue: "",

      eyeValue: "",
      genderValue: "",
      openDialog: false,
      openDialogReg: false,
      openDialogAuth: false,
      successfulAuth: false,

      modelPerson: {},
      modelUser: {},
      modelFavPerson: {},

      favouriteWiz: [],
      favouriteNoWiz: [],
    };
  },
  methods: {
    async getPersons() {
      let result = await fetch("https://hp-api.onrender.com/api/characters");
      this.persons = await result.json();
    },
    getSelOpt(value) {
      this.selectedValue = value;
    },
    getSearchVal(value) {
      this.searchValue = value;
    },
    updateValueGender(value) {
      this.genderValue = value;
    },
    updateValueEye(value) {
      this.eyeValue = value;
    },
    updateDialogValue(value, person) {
      this.openDialog = value;
      this.modelPerson = person;
    },
    closeModal(value) {
      this.openDialog = value;
    },
    successAuth(value) {
      this.modelUser = value;
    },
    favourPerson(value) {
      this.modelFavPerson = value;
      if (this.modelFavPerson.wizard === true) {
        this.favouriteWiz.push(this.modelFavPerson);
      }
      if (this.modelFavPerson.wizard === false) {
        this.favouriteNoWiz.push(this.modelFavPerson);
      }
    },
    favourPersonDel(value) {
      this.modelFavPerson = value;
      if (this.modelFavPerson.wizard === true) {
        this.favouriteWiz.splice(
            this.favouriteWiz.indexOf(this.modelFavPerson),
            1
        );
      }
      if (this.modelFavPerson.wizard === false) {
        this.favouriteNoWiz.splice(
            this.favouriteNoWiz.indexOf(this.modelFavPerson),
            1
        );
      }
    },
  },
  computed: {
    sortedPersonsPosts() {
      console.log(this.selectedValue);
      if (this.selectedValue.includes("Reverse")) {
        return [...this.persons]
            .sort((pers1, pers2) =>
                pers1[this.selectedValue.replace("Reverse", "")]?.localeCompare(
                    pers2[this.selectedValue.replace("Reverse", "")]
                )
            )
            .reverse();
      } else {
        return [...this.persons].sort((pers1, pers2) =>
            pers1[this.selectedValue]?.localeCompare(pers2[this.selectedValue])
        );
      }
    },
    searchPersonsPosts() {
      return this.sortedPersonsPosts.filter(
          (post) =>
              post.name.toLowerCase().includes(this.searchValue.toLowerCase()) ||
              post.ancestry
                  .toLowerCase()
                  .includes(this.searchValue.toLowerCase()) ||
              post.house.toLowerCase().includes(this.searchValue.toLowerCase())
      );
    },
    sortedPersonsGender() {
      if (this.genderValue === "") {
        return this.searchPersonsPosts;
      } else {
        return this.searchPersonsPosts.filter(
            (post) => post.gender === this.genderValue
        );
      }
    },
    sortedPersonsEye() {
      if (this.eyeValue === "") {
        return this.sortedPersonsGender;
      } else {
        return this.sortedPersonsGender.filter(
            (post) => post.eyeColour === this.eyeValue
        );
      }
    },
  },
  mounted() {
    this.getPersons();
  },
};
</script>

<style scoped>
.main-block {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.dialogWindow {
  position: fixed;
  background: transparent;
  padding: 20px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(0, 0, 0, 0.5);
  margin: 0;
  padding: 0;
}

.main-block__header {
  display: flex;
}

.btn-reg {
  width: 100px;
  height: 30px;
  align-self: end;
  background: coral;
  color: whitesmoke;
  border: 2px solid #cb5932;
  margin: 8px 16px;
}

.filters {
  display: flex;
  flex-direction: column;
  margin-right: 420px;
}

.favourites {
  border: #cb5932 3px solid;
  padding: 5px 10px;
  position: absolute;
  margin-left: 600px;
  margin-top: 100px;
}
.dialogRegistration,
.dialogAuth{
  background: #ffffff;
  box-shadow: #cb5932 7px 7px 10px 7px;
  border: 0;
}
</style>
