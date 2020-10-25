<template>
  <base-dialog v-if="isInvalidInput" title="Invalid input" @close="closeDialog">
    <template #default>
      <p>All fields are required. Please insert data.</p>
    </template>
    <template #actions>
      <base-button @click.prevent="closeDialog">Ok, close</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="descrInput" />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" ref="linkInput" />
      </div>
      <div class="form-control">
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      isInvalidInput: false
    };
  },
  methods: {
    submitResource() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descrInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.isInvalidInput = true;
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
    closeDialog() {
      this.isInvalidInput = false;
    }
  }
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