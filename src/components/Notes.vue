<script>
export default {
  name: 'Notes',
  data() {
    return {
      savesText: '',
      text: 'Add your notes',
    };
  },
  props: {
    selectedItem: Object,
    closeModal: Function,
  },
  mounted() {
    const notesText = this.selectedItem.notes;

    if (notesText) {
      this.savesText = notesText;
      this.text = notesText;
    }
  },
  methods: {
    undo() {
      this.text = this.savesText;
    },
    saveNotes() {
      const updatedItem = {
        ...this.selectedItem,
        notes: this.text,
      };

      this.closeModal(updatedItem);
    },
  },
};
</script>

<template>
  <div class="Notes">
    <textarea
      name="notes"
      cols="30"
      rows="10"
      class="Notes-textarea"
      v-model="text"
    ></textarea>

    <div class="Notes_buttons">
      <button
        class="btn btn_undo-notes"
        @click="undo"
      >
        Undo
      </button>

      <button
        class="btn btn_save-notes"
        @click="saveNotes"
      >
        Save
      </button>

    </div>

    <button
      class="btn btn-close-modal"
      @click="closeModal"
    >
      ×
    </button>
  </div>
</template>

<style scoped>
  .Notes {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;

    padding: 80px 100px;

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    background-color: rgba(0, 0, 0, 0.5);
    z-index: 2;
  }

  .Notes-textarea {
    width: 100%;
    height: 100%;
    padding: 10px 15px;

    background-color: #fff;
  }

  .Notes_buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;

    margin-top: 20px;
  }

  .btn_save-notes,
  .btn_undo-notes {
    min-width: 30%;

    color: #fff;
    font-size: 20px;
    font-weight: 600;
  }

  .btn_save-notes {
    background-color: green;
  }

  .btn_undo-notes {
    background-color: red;
  }
</style>
