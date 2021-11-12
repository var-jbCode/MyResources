<template>
  <base-dialog
    v-if="isInputInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunatley at least on input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        charatcers into each.
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">OK</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="Description">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="Description">Description</label>
        <textarea
          id="Description"
          name="Description"
          type="text"
          rows="3"
          ref="descInput"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../base/BaseButton.vue';
export default {
  components: { BaseButton },
  data() {
    return {
      isInputInvalid: false,
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDesc = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDesc.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.isInputInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDesc, enteredLink);
    },
    confirmError() {
      this.isInputInvalid = false;
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
  color: #41b883;
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}
input:focus,
textarea:focus {
  color: #41b883;
  outline: none;
  border-color: #41b883;
  background-color: #34495e;
}
.form-control {
  margin: 1rem 0;
}
</style>
