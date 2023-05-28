<template>
  <form action="" class="form-auth">
    <strong>Авторизация</strong>
    <BtnClose @click.prevent="$emit('closeAuth', false)">Закрыть</BtnClose>
    <input class="inp-auth" type="text" v-model="inpLoginAuth" placeholder="Введите логин" name="" id="">
    <input class="inp-auth" type="text" v-model="inpPassAuth" placeholder="Введите пароль" name="" id="">
    <BtnCome class="btn-auth" @click.prevent="loginUser">Вход</BtnCome>
  </form>
</template>

<script>
import BtnClose from "@/UI/buttons/BtnClose.vue";
import BtnCome from "@/UI/buttons/BtnCome.vue";

export default {
  components: {BtnCome, BtnClose},
  data() {
    return {
      inpLoginAuth: '',
      inpPassAuth: ''
    }
  },
  methods: {
    loginUser() {
      for (let i = 0; i < localStorage.length; i++) {
        let id = localStorage.key(i)
        let value = localStorage[id]
        let user = JSON.parse(value)
        if (user.login === this.inpLoginAuth && user.password === this.inpPassAuth) {
          this.$emit('succesAuth', true)
          let sendUser = {
            name: user.name,
            fam: user.fam,
            otch: user.otch
          }
          this.$emit('sendUser', sendUser)
          console.log('naiden')
          this.$emit('closeAuthWind', false)
          this.inpLoginAuth = ''
          this.inpPassAuth = ''
          break;
        } else {
          console.log('ne naiden')
        }
      }
    }
  }
}
</script>

<style scoped>
.form-auth {
  display: flex;
  flex-direction: column;
  width: 300px;
  height: 150px;
  align-items: center;
  justify-content: space-around;
  padding: 20px;
}

.inp-auth {
  width: 200px;
  height: 30px;
  margin: 5px 0;
}

.btn-auth {
  width: 100px !important;
}

strong {
  font-size: 20px;
  color: #ff4700;
  margin-bottom: 10px;
}
</style>