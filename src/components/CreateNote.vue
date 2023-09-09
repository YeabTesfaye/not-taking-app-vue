<template>
  <div class="ui basic content center aligned segment">
    <h2 class="ui header">My Note-Taking App</h2>
    <button class="ui basic button icon" v-on:click="showModel">
      <i class='plus icon'></i>
    </button>
    <div class="ui centered card" v-show="shhielemnt">
      <div class="content">
        <div class="ui form">
          <div class='field'>
            <label>Title</label>
            <input type='text' v-model="titleT">
          </div>
          <div class='field'>
            <label>Description</label>
            <input type='text' v-model="descriptionText">
          </div>
          <div class='ui two buttons'>
            <button class='ui basic green button' v-on:click="SendDataModel">
              Create
            </button>
            <button class='ui basic black button' v-on:click="closeModel">
              Cancel
            </button>
          </div>
        </div>
        <div class="ui error message" v-if="error">
          <div class="header">Error</div>
          <p>Please enter both a title and a description.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titleT: "",
      descriptionText: "",
      shhielemnt: false,
      error: false, // Add an error property to track validation errors
    };
  },
  methods: {
    showModel() {
      this.shhielemnt = true;
      this.error = false; // Reset the error message when the model is shown
    },
    closeModel() {
      this.shhielemnt = false;
    },
    SendDataModel() {
      if (this.titleT.length > 0 && this.descriptionText.length > 0) {
        const title = this.titleT;
        const description = this.descriptionText;

        this.$emit('SeDataToCnote', {
          title,
          description,
        });

        // Clean fields
        this.titleT = "";
        this.descriptionText = "";
        this.shhielemnt = false;
      } else {
        // Show the error message if either title or description is empty
        this.error = true;
      }
    },
  },
};
</script>
