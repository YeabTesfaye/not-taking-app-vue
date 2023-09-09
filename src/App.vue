<template>
  <CreateNote v-on:SeDataToCnote="CreateNote" />
  <ListNote :notesd="notes" />
</template>

<script>
import CreateNote from "./components/CreateNote.vue";
import ListNote from "./components/ListNotes.vue";

export default {
  name: "App",
  components: {
    CreateNote,
    ListNote,
  },
  data() {
    return {
      notes: [],
    };
  },
  mounted() {
    const storedNotes = localStorage.getItem("notes"); // Use "notes" as the key
    if (storedNotes) {
      this.notes = JSON.parse(storedNotes);
    }
  },
  methods: {
    CreateNote(note) {
      this.notes.push(note);
      localStorage.setItem("notes", JSON.stringify(this.notes)); // Use "notes" as the key
    },

    deleteNote(note) {
      console.log(note);
      const index = this.notes.indexOf(note);
      if (index !== -1) {
        this.notes.splice(index, 1); 
        console.log(index);
      }
      localStorage.setItem("notes", JSON.stringify(this.notes)); // Use "notes" as the key
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
