<template>
  <base-dialog v-if="isEditClicked">
    <div class="form-control">
      <label for="title">Edit Title</label>
      <input type="text" name="title" id="title" v-model="newTitle" />
    </div>
    <div class="form-control">
      <label for="Edit description">Description</label>
      <textarea
        name="description"
        id="description"
        rows="3"
        v-model="newDescription"
      ></textarea>
    </div>
    <div class="form-control">
      <label for="link">Edit Link</label>
      <input type="url" name="link" id="link" v-model="newLink" />
    </div>
    <div>
      <base-btn @click="handleEdit">Save</base-btn>
    </div>
  </base-dialog>

  <li>
    <base-card class="card">
      <div id="desc">
        <header>
          <h3>{{ title }}</h3>
        </header>
        <p>{{ description }}</p>
        <nav>
          <a :href="link" target="_blank">View Resource</a>
        </nav>
      </div>
      <div id="actions">
        <base-btn @click="deleteResource(id)">Delete</base-btn>
        <base-btn @click="isEditClicked = true">Edit</base-btn>
      </div>
    </base-card>
  </li>
</template>

<script>
export default {
  props: ['id', 'title', 'description', 'link'],
  inject: ['deleteResource', 'editResource'],
  data() {
    return {
      isEditClicked: false,
      newTitle: this.title,
      newDescription: this.description,
      newLink: this.link,
    };
  },
  methods: {
    handleEdit() {
      this.editResource(
        this.id,
        this.newTitle,
        this.newDescription,
        this.newLink
      );
      this.isEditClicked = false;
    },
  },
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
  transition: ease-out 4s;
}

.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  text-align: justify;
  padding: 1rem 0;
  margin: 0.5rem 0;
}

a {
  border-radius: 10px;
  text-decoration: none;
  color: #ce5c00;
  font-weight: bold;
}

a:hover,
a:active {
  color: #c89300;
}

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

#actions {
  max-width: 200px;
  display: flex;
  flex-direction: column-reverse;
  justify-content: space-between;
}

#actions button{
  margin: 5px 2px;
}

</style>