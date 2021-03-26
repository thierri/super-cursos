<template>
  <div class="flex content-center fixed inset-0 bg-gray-100">
    <form @submit.prevent="userLogin" class=" bg-white border m-auto p-10 rounded shadow-lg space-y-6">
      <div>
        <label class="block mb-2">Username</label>
        <input class="border p-2 " type="text" v-model="login.username" />
      </div>
      <div >
        <label class="block mb-2">Password</label>
        <input class="border p-2" type="text" v-model="login.password" />
      </div>
      <div>
        <button class="p-2 w-full bg-indigo-500 text-white" type="submit">Entrar</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      login: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith('local', { data: this.login })
        console.log(response)
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>