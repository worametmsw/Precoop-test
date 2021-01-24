<template>
  <div class="h-screen bg-cover login flex justify-center">
    <div class="flex bg-gray mt-10 py-10 mb-40 px-1 rounded-xl" v-show="showSelect">
      <div class="container mr-3 py-1 max-w-md mx-auto">
        <label class="font-semibold text-sm text-gray-600 pb-1 block">Name English</label>
        <v-select
          id="movie"
          v-model="movieName"
          :options="movieNameOption"
          :clearable="false"
          placeholder="เลือกหนัง"
          class="select"
        />
        <label class="font-semibold text-sm text-gray-600 pb-1 block">Name Movie English</label>
        <input
          v-model="showEn"
          disabled
          type="text"
          class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
          placeholder="Name English"
        />
        <label class="font-semibold text-sm text-gray-600">Name Movie Thailand </label>
        <input
          v-model="showTh"
          disabled
          type="text"
          class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
          placeholder="Name Thailand"
        />
        <label class="font-semibold text-sm text-gray-600 pb-1 block">Year Movie</label>
        <input
          v-model="showYear"
          disabled
          type="text"
          class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
          placeholder="Year Movie"
        />
        <div class="container mr-3 py-1 max-w-md mx-auto">
          <button @click="search" type="button" class="bg-blue rounded px-3 py-3 hover:bg-green mr-2 text-white">
            SEARCH
          </button>
          <button @click="addMovie" type="button" class="bg-blue rounded px-2 py-3 hover:bg-green mr-2 text-white">
            ADD MOVIE
          </button>
          <button
            @click="edit"
            type="button"
            class="bg-blue rounded px-2 py-3 hover:bg-green mr-2 text-white"
            v-show="showEditbutton"
          >
            Edit Movie
          </button>
        </div>
        <NuxtLink to="/"><button class="bg-danger w-full rounded px-2 py-3 mt-6 text-white">LogOut</button></NuxtLink>
      </div>
    </div>

    <div class="p-10 xs:p-0 mx-auto md:w-full md:max-w-md" v-show="showMovie">
      <div class="flex bg-gray mt-10 py-10 mb-40 px-1 rounded-xl">
        <h1 class="font-bold text-center text-2xl mb-5">ADD MOVIE</h1>
        <div class="px-5 py-7">
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Name English</label>
          <input
            v-model="setEnname"
            type="text"
            class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
            placeholder="Name English"
          />
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Name Thailand</label>
          <input
            v-model="setThname"
            type="text"
            class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
            placeholder="Name Thailand"
          />
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Year Movie</label>
          <input
            v-model="setYear"
            type="number"
            class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
            placeholder="Year Movie"
          />
          <button
            @click="save"
            type="button"
            class="bg-blue hover:bg-green text-white w-full py-4 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block mt-3"
          >
            <span class="inline-block mr-2">Save</span>
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

    <div class="p-10 xs:p-0 mx-auto md:w-full md:max-w-md" v-show="editshow">
      <div class="flex bg-gray mt-10 py-10 mb-40 px-1 rounded-xl">
        <h1 class="font-bold text-center text-2xl mb-5">Edit Movie</h1>
        <div class="px-5 py-7">
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Name English</label>
          <input
            v-model="editEng"
            type="text"
            class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
            placeholder="Name English"
          />
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Name Thailand</label>
          <input
            v-model="editTh"
            type="text"
            class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
            placeholder="Name Thailand"
          />
          <label class="font-semibold text-sm text-gray-600 pb-1 block">Year Movie</label>
          <input
            v-model="editYear"
            type="number"
            class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
            placeholder="Year Movie"
          />
          <button
            @click="Editsave"
            type="button"
            class="bg-blue hover:bg-green text-white w-full py-4 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block mt-3"
          >
            <span class="inline-block mr-2">Save</span>
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
import Vue from 'vue'
import vSelect from 'vue-select'
import 'vue-select/dist/vue-select.css'
Vue.component('v-select', vSelect)
export default {
  data() {
    return {
      movieName: '',
      showEn: '',
      showTh: '',
      showYear: '',
      showSelect: true,
      showMovie: false,
      editshow: false,
      showEditbutton: false,
      setEnname: '',
      setThname: '',
      setYear: '',
      movieNameOption: [
        {
          nameEn: 'Avenger',
          nameTh: 'อเวนเจอร์',
          year: '2010',
          label: 'Avenger'
        },
        {
          nameEn: 'Spiderman 3',
          nameTh: 'สไปเดอร์แมน 3',
          year: '2015',
          label: 'Spiderman 3'
        }
      ]
    }
  },
  methods: {
    search() {
      this.showEn = this.movieName.nameEn
      this.showTh = this.movieName.nameTh
      this.showYear = this.movieName.year
      if (this.movieName !== '') {
        this.showEditbutton = true
      }
    },
    save() {
      if (this.setEnname !== '' && this.setThname !== '' && this.setYear) {
        const n = {
          nameEn: this.setEnname,
          nameTh: this.setThname,
          year: this.setYear,
          label: this.setEnname
        }
        this.movieNameOption.push(n)
        this.setEnname = ''
        this.setThname = ''
        this.setYear = ''
        alert('Success')
        this.showMovie = false
        this.showSelect = true
      } else {
        alert('Add Movie Fail')
      }
    },
    Editsave() {
      if (this.editEng !== '' && this.editTh !== '' && this.editYear) {
        this.movieName.nameEn = this.editEng
        this.movieName.nameTh = this.editTh
        this.movieName.year = this.editYear
        this.movieName.label = this.editEng
        this.editshow = false
        this.showSelect = true
      }
      this.setEnname = ''
      this.setThname = ''
      this.setYear = ''
      this.search()
    },
    back() {
      this.showSelect = true
      this.showMovie = false
      this.editshow = false
    },
    addMovie() {
      this.showMovie = true
      this.showSelect = false
    },
    edit() {
      this.editshow = true
      this.showSelect = false
      this.editEng = this.showEn
      this.editTh = this.showTh
      this.editYear = this.showYear
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
