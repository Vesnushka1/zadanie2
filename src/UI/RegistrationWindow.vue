<template>
  <form action="" class="form-reg">
    <strong>Регистрация</strong>
    <BtnClose @click.prevent="$emit('closeReg', false)">X</BtnClose>
    <input v-model="inpLogin" type="text" placeholder="Введите логин" name="" id="">
    <input v-model="inpPass" type="text" placeholder="Введите пароль" name="" id="">
    <input v-model="inpFam" type="text" placeholder="Фамилия" name="" id="">
    <input v-model="inpName" type="text" placeholder="Имя" name="" id="">
    <input v-model="inpOtch" type="text" placeholder="Отчество" name="" id="">
    <input v-model="inpTel" type="text" placeholder="Телефон" name="" id="">
    <input v-model="inpAge" type="text" placeholder="Введите возраст" name="" id="">
    <div class="col">
      <span>Ваш пол:</span>
      <label for="genderIdM"><input type="radio" name="gender" id="genderIdM"> Мужской</label>
      <label for="genderIdW"><input type="radio" name="gender" id="genderIdW"> Женский</label>
    </div>
    <div class="col">
      <span>Любимый факультет в Хогвартсе:</span>
      <label for="facultyIdG"><input type="checkbox" name="faculty" id="facultyIdG">Гриффиндор</label>
      <label for="facultyIdK"><input type="checkbox" name="faculty" id="facultyIdK">Когтевран</label>
      <label for="facultyIdP"><input type="checkbox" name="faculty" id="facultyIdP">Пуффендуй</label>
      <label for="facultyIdS"><input type="checkbox" name="faculty" id="facultyIdS">Слизерин</label>
    </div>
    <BtnCome @click.prevent="storageRoom">Зарегистрироваться</BtnCome>
  </form>
</template>

<script>

import BtnClose from "@/UI/buttons/BtnClose.vue";
import BtnCome from "@/UI/buttons/BtnCome.vue";

export default {
  components: {BtnCome, BtnClose},
  data() {
    return {
      inpLogin: '',
      inpPass: '',
      inpFam: '',
      inpName: '',
      inpOtch: '',
      inpTel: '',
      inpAge: '',
      gender: '',
      arrayFaculty: [],

      check: false,

    }
  },
  methods: {
    // checkReg() {
    //   if (this.inpFam.test(/[А-Я][а-я]{1,}/)) {
    //     this.check = true
    //     console.log('Фам верно')
    //   } else {
    //     console.log('Введите правильную фамилию')
    //   }
    // if (this.inpName.test(/a/)) {
    //   this.check = true
    // } else {
    //   console.log('Введите правильную имя')
    // }
    // if (this.inpOtch.test(/a/)) {
    //   this.check = true
    // } else {
    //   console.log('Введите правильную отчество')
    // }
    storageRoom() {
      //if (this.check === true) {
      let id = Date.now()
      let objReg = {
        login: this.inpLogin,
        password: this.inpPass,
        fam: this.inpFam,
        name: this.inpName,
        otch: this.inpOtch,
        tel: this.inpTel,
        age: this.inpAge,
        gender: this.gender,
        faculty: this.arrayFaculty
      }
      localStorage.setItem(id.toString(), JSON.stringify(objReg))
      this.inpLogin = ''
      this.inpPass = ''
      this.inpFam = ''
      this.inpName = ''
      this.inpOtch = ''
      this.inpTel = ''
      this.inpAge = ''
      this.gender = ''
      this.arrayFaculty = []
      this.$emit('closeRegAfterReg', false)
    }
    //}
  }
}
</script>

<style scoped>
.form-reg {
  display: flex;
  flex-direction: column;
  padding: 20px;
  width: 400px;
  align-items: center;
}

input[type='text'] {
  width: 270px;
  height: 25px;
  margin: 5px 0;
}
input[type='checkbox'] {
  margin: 7px 10px 10px 0
}

strong {
  font-size: 20px;
  color: #ff4700;
  margin-bottom: 10px;
}

.col {
  display: flex;
  flex-direction: column;
  margin: 15px 0 15px 65px;
  align-self: start;
}
</style>