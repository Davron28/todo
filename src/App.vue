<template>
  <Navbar 
  @searchValue="search = $event"
  :lang="lang"
  @changeLang="changeLang"
  />
  <Notes 
  :lang="lang"
  :notes="filterNotes"
  @delNote="deleteNote"
  @changeNote="changeNote"
  />
  <Modal 
  :currentId="currentId"
  v-show="modalOpen"
  @closeModal="closeModal"
  @addNote="addNote"
  :editNote="editNote"
  :edit="edit"
  @editedNote="editedNote"
  :lang="lang"
  />
  <Button 
  @openModal="openModal"
  :modalOpen="modalOpen"/>
</template>

<script>
import Navbar from "@/components/Navbar.vue"
import Notes from "@/components/Notes.vue"
import Modal from "@/components/Modal.vue"
import Button from "@/components/Button.vue"
import langs from "@/lang"
export default {
  created() {
    this.getNotes();
    localStorage.lang = localStorage.lang || "ru"
    this.lang = localStorage.lang || "ru"
    this.langwords = langs
    localStorage.words = JSON.stringify(this.langwords)
  },
  watch: {
    notes: {
      handler(newNotes) {
        localStorage.notes = JSON.stringify(this.notes);
      },
      deep: true
    }
  },
  computed: {
    filterNotes() {
      return this.search ? this.notes.filter(note => note.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes;
    }
  },
  components: {
    Navbar,
    Notes,
    Modal,
    Button
  },
  data() {
    return {
      notes: [],
      currentId: 1,
      modalOpen: false,
      edit: false,
      editNote: {},
      lang: "ru",
      langwords: {},
      search: ""
    }
  },
  methods: {
    openModal() {
      this.modalOpen = true
      this.edit = false
    },
    closeModal(status) {
      this.modalOpen = status
    },
    addNote(item) {
      this.notes.push(item)
      this.modalOpen = false
    },
    deleteNote(id) {
      let index = this.notes.findIndex(note => note.id == id)
      this.notes.splice(index, 1)
    },
    changeNote(id) {
      this.edit = this.modalOpen = true
      let pickedNote = this.notes.find(note => note.id == id);
      this.editNote = pickedNote
    },
    editedNote(editeNote) {
      this.notes.forEach(note => {
        if(note.id == editeNote.id) {
          note.title = editeNote.title
          note.descr = editeNote.descr
          note.date = editeNote.date
        }
      })
      this.edit = false
    },
    getNotes() {
      const localNotes = localStorage.notes;
      if(localNotes) {
        this.notes = JSON.parse(localNotes)
      }
    },
    changeLang(val) {
      this.lang = localStorage.lang = val
    }
  },
  provide() {
    return {
      words: localStorage.words ? JSON.parse(localStorage.words) : {}
    }
  }
}
</script>

<style>

</style>