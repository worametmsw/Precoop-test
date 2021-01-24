<template>
  <div class="min-h-screen bg-gray-100 flex flex-col justify-center sm:py-12 login">
    <div v-show="showLogin" class="rounded-xl bg-gray p-10 xs:p-0 mx-auto md:w-full md:max-w-md">
      <h1 class="font-bold text-center text-2xl mb-5">Your Login</h1>
      <div class="bg-white shadow w-full rounded-lg divide-y divide-gray-200">
        <div class="px-5 py-8  bg-orange rounded">
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Username</label>
          <input v-model="username" type="text" class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full" placeholder="username" />
          <label class="font-semibold text-sm text-gray-600 pb-1 block" >Password</label>
           <input v-model="password" class="shadow appearance-none border border-red rounded w-full py-2 px-3 text-grey-darker mb-3" id="password" type="password" placeholder="******************">
          <button
            @click="login"
            type="button"
            class="bg-blue hover:bg-green text-white w-full py-4 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block"
          >
            <span class="inline-block mr-2">Login</span>
          </button>
          <button
            @click="clickRegister"
            type="button"
            class="bg-blue hover:bg-green text-white w-full py-4 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block mt-3"
          >
            <span class="inline-block mr-2">Register</span>
          </button>
        </div>
      </div>
    </div>

    <div class="p-4 xs:p-0 mx-auto md:w-full md:max-w-md " v-show="showRegister">
      <div class="bg-white shadow w-full rounded-lg divide-y divide-gray-200">
        <div class="px-5 py-7 p-4 xs:p-0 mx-auto md:w-full md:max-w-md">
          <h1 class="font-bold text-center text-2xl mb-3">Register</h1>
          <label class="font-semibold text-sm text-gray-600 pb-1 block ">username</label>
          <input v-model="setUsername" type="text" class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full" placeholder="username" />
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Password</label>
          <input v-model="setPassword" type="password" class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full" placeholder="password" />
          <button
            @click="summit"
            type="button"
            class="bg-blue hover:bg-green text-white w-full py-4 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block mt-3"
          >
            <span class="inline-block mr-2">Summit</span>
          </button>
          <button
            @click="back"
            type="button"
            class="bg-blue hover:bg-green text-white w-full py-4 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block mt-3"
          >
            Back
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      setUsername: '',
      setPassword: '',
      showRegister: false,
      showLogin: true
    }
  },
  methods: {
    redirect(value) {
      this.$router.push({ path: value })
    },
    login() {
      if (this.username === this.setUsername && this.password === this.setPassword && this.username !== '' && this.password !== '') {
        alert('Login Success')
        this.redirect('/admin')
      } else {
        alert('Login Fail')
      }
      console.log(this.username)
      console.log(this.password)
    },
    clickRegister() {
      this.showRegister = true
      this.showLogin = false
    },
    back() {
      this.showLogin = true
      this.showRegister = false
    },
    summit() {
      if (this.setUsername === '' || this.setPassword === '') {
        alert('Register Fail')
      } else {
        alert('Register Success')
        this.showLogin = true
        this.showRegister = false
      }
      console.log(this.setUsername)
      console.log(this.setPassword)
    }
  }
}
</script>

<style scoped>
.select {
  height: 38px;
  width: 150px;
  margin-right: 10px;
}
.login {
  /*
    background: url('https://tailwindadmin.netlify.app/dist/images/login-new.jpeg');
  */
  background: url('http://bit.ly/2gPLxZ4');
  background-repeat: no-repeat;
  background-size: cover;
}
</style>