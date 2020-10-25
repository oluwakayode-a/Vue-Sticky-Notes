<template>
  <div class="m-auto max-w-6xl">
    <h1 class="text-3xl font-bold text-center mx-8 my-8">
      <span class="fa fa-book text-blue-500"></span>
      My <span class="text-blue-500">Sticky</span>Notes
    </h1>

    <form class="mx-8" @submit.prevent="addNote">
      <label for="title" class="block mb-2 text-gray-800 font-semibold">
        Title
      </label>
       <input type="text" v-model="title" name="title" id="title" required class="border w-full px-3 py-2 appearance-none focus:outline-none focus:shadow-outline">

      <p class="mt-3">
         Note Color <span class="inline-block px-2 py-1 text-white rounded-lg" :class="bg">{{ bg }}</span>)
      </p>

      <div class="flex mt-3">
        <select name="bgColor" id="bgColor" v-model="bg">
          <option class="w-5 h-3 focus:outline-none focus:shadow-outline ml-2 bg-blue-500" id="bg-blue-500">bg-blue-500</option>
          <option class="w-5 h-3 focus:outline-none focus:shadow-outline bg-blue-800" id="bg-blue-800">bg-blue-800</option>
          <option class="w-5 h-3 focus:outline-none focus:shadow-outline ml-2 bg-green-500" id="bg-green-500">bg-green-500</option>
          <option class="w-5 h-3 focus:outline-none focus:shadow-outline ml-2 bg-orange-600" id="bg-orange-600">bg-orange-600</option>
          <option class="w-5 h-3 focus:outline-none focus:shadow-outline ml-2 bg-red-500" id="bg-red-500">bg-red-500</option>
        </select>
      </div>

      <label for="note" class="block mt-4 text-gray-800 font-semibold">Note</label>
      <textarea name="note" v-model="note" id="note" cols="30" rows="10" maxlength="200" required class="border mt-2 px-3 py-2 w-full appearance-none focus:outline-none focus:shadow-outline"></textarea>

      <button type="submit" class="bg-blue-500 px-3 py-2 w-full text-white font-semibold mt-4 focus:shadow-outline focus:outline-none hover:bg-blue-700">Add Note</button>
    </form>

    <div class="flex mx-8 my-3 flex-col sm:flex-row flex-wrap flex-grow justify-evenly">
      <Note :note="entry" :index='index' :deleteNote='deleteNote' ref="note" v-for="(entry, index) in notes" :key="index" />
    </div>
  </div>
</template>

<script>
import Note from './Note'
export default {
  name: 'Notes',
  components: {
    Note
  },
  data() {
    return {
      title: '',
      note: '',
      bg: 'bg-blue-500',
      notes: []
    }
  },
  methods: {
    addNote() {
      // console.log(title, note, bgColor);
      // Add Note
      this.notes.push({'title' : this.title, 'note' : this.note, 'bg' : this.bg})

      // Add to LocalStorage
      localStorage.setItem('notes', JSON.stringify(this.notes));

      // Clear inputs
      this.title = ''
      this.note = ''
      this.bg = 'bg-blue-500'
    },
    deleteNote(index) {
      this.notes.splice(index, 1)

      // Remove from LocalStorage
      localStorage.setItem('notes', JSON.stringify(this.notes))
    }
  },
  mounted() {
    // Load Notes on Page Load
    if (localStorage.getItem('notes') == null ) {
      this.notes = []
    } else {
      this.notes = JSON.parse(localStorage.getItem('notes'))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.0-2/css/all.min.css";

</style>
