<script>
export default {
  name: 'RelatedInfo',
  data() {
    return {
      savesText: '',
      text: 'Add your related info',
    };
  },
  props: {
    selectedItem: Object,
    closeModal: Function,
  },
  mounted() {
    const infoText = this.selectedItem.info;

    if (infoText) {
      this.savesText = infoText;
      this.text = infoText;
    }
  },
  methods: {
    undo() {
      this.text = this.savesText;
    },
    saveInfo() {
      const updatedItem = {
        ...this.selectedItem,
        info: this.text,
      };

      this.closeModal(updatedItem);
    },
  },
};
</script>

<template>
  <div class="Info">
    <textarea
      name="info"
      cols="30"
      rows="10"
      class="Info-textarea"
      v-model="text"
    ></textarea>

    <div class="Info_buttons">
      <button
        class="btn btn_undo-info"
        @click="undo"
      >
        Undo
      </button>

      <button
        class="btn btn_save-info"
        @click="saveInfo"
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
  .Info {
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

  .Info-textarea {
    width: 100%;
    height: 100%;
    padding: 10px 15px;

    background-color: #fff;
  }

  .Info_buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;

    margin-top: 20px;
  }

  .btn_save-info,
  .btn_undo-info {
    min-width: 30%;

    color: #fff;
    font-size: 20px;
    font-weight: 600;
  }

  .btn_save-info {
    background-color: green;
  }

  .btn_undo-info {
    background-color: red;
  }
</style>
