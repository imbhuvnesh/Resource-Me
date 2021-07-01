<template>
  <base-dialog v-if="isInvalid" title="Invalid Input">
    <template #default>
      <p>Unfortunately, Atleast one input value is invalid!</p>
      <p>Please check input field again!</p>
    </template>
    <template #actions>
      <base-btn @click="isInvalid = !isInvalid">Okay</base-btn>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" ref="linkInput" />
      </div>
      <div>
        <base-btn type="Submit">Add Resource</base-btn>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      isInvalid: false,
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enterdLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enterdLink.trim() === ''
      ) {
        this.isInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enterdLink);
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>