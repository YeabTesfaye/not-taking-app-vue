<template>
  <div class="ui cards" v-if="notesd && notesd.length > 0">
    <tnotes
      v-on:DeleteN="deleteNoteSE"
      v-for="(note, index) in notesd"
      :key="index"
      :notesL="note"
    />
  </div>
</template>
<script>
import Tnotes from "./TextNote.vue";
export default {
  props: ["notesd"],
  components: {
    Tnotes,
  },
  methods: {
    deleteNoteSE(note) {
      var ifRemove = confirm("Do you really want to delete the note");
      if (ifRemove) {
        const indexOFNote = this.notesd.indexOf(note);
        this.notesd.splice(indexOFNote, 1);
        localStorage.setItem('notes', JSON.stringify(this.notesd))
      }
    },
  },
};
</script>

<style scoped>
.ui.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1.5rem;
}
</style>
