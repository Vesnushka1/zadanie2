<template>
  <form action="" class="form-auth">
    <button @click.prevent="$emit('closeAuth', false)">Закрыть</button>
    <input type="text" v-model="inpLoginAuth" placeholder="Введите логин" name="" id="">
    <input type="text" v-model="inpPassAuth" placeholder="Введите пароль" name="" id="">
    <button @click.prevent="loginUser">Вход</button>
  </form>
</template>

<script>
export default {
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
}
</style>