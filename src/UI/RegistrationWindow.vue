<template>
  <form action="" class="form-reg">
    <button @click.prevent="$emit('closeReg', false)">Закрыть</button>
    <input v-model="inpLogin" type="text" placeholder="Введите логин" name="" id="">
    <input v-model="inpPass" type="password" placeholder="Введите пароль" name="" id="">
    <input v-model="inpFam" type="text" placeholder="Фамилия" name="" id="">
    <input v-model="inpName" type="text" placeholder="Имя" name="" id="">
    <input v-model="inpOtch" type="text" placeholder="Отчество" name="" id="">
    <input v-model="inpTel" type="number" placeholder="Телефон" name="" id="">
    <input type="radio" name="gender" id="genderId"><label for="genderId">Мужской</label>
    <input type="radio" name="gender" id="genderId"><label for="genderId">Женский</label>
    <input v-model="inpAge" type="text" placeholder="Введите возраст" name="" id="">
    <input type="checkbox" name="faculty" id="facultyId"><label for="facultyId">Гриффиндор</label>
    <input type="checkbox" name="faculty" id="facultyId"><label for="facultyId">Когтевран</label>
    <input type="checkbox" name="faculty" id="facultyId"><label for="facultyId">Пуффендуй</label>
    <input type="checkbox" name="faculty" id="facultyId"><label for="facultyId">Слизерин</label>
    <button @click.prevent="storageRoom">Зарегистрироваться</button>
  </form>
</template>

<script>

export default {
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
}
</style>