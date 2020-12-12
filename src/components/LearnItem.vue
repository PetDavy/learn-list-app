<script>
export default {
  name: 'LearnItem',
  props: {
    item: Object,
    removeLearn: Function,
    openNotes: Function,
    openInfo: Function,
  },
  data() {
    return {
      styleObjectNotes: {
        hasNotes: this.item.notes,
      },
      styleObjectInfo: {
        hasInfo: this.item.info,
      },
    };
  },
};
</script>

<template>
  <li class="LearnItem">
    <span>
      {{item.title}}
    </span>

    <div class="LearnItem_buttons">
      <button
        class="btn btn_add-related"
        :class="styleObjectInfo"
        @click="openInfo(item.id)"
      >
        <i class="fas fa-plus"></i>
        Add Info
      </button>

      <button
        class="btn"
        @click="openNotes(item.id)"
        :class="styleObjectNotes"
      >
        <i class="fas fa-book-open"></i>
        Notes
      </button>

      <button
        type="button"
        class="btn btn-remove"
        @click="removeLearn(item.id)"
      >
        <i class="fas fa-trash"></i>
        Remove
      </button>
    </div>
  </li>
</template>

<style scoped>
  .LearnItem {
    display: flex;
    justify-content: space-between;
    align-items: center;

    margin-bottom: 10px;
    padding: 15px 20px;

    font-size: 19px;
    font-weight: 600;
    background-color: #fff;
    border-radius: 4px;
  }

  .LearnItem_buttons {
    display: flex;
  }

  .LearnItem_buttons .btn {
    border: none;
    background-color: transparent;
    font-size: 17px;
    color: #bedac6;
  }

  .LearnItem_buttons i {
    margin-right: 5px;
  }

  .LearnItem_buttons .hasNotes,
  .LearnItem_buttons .hasInfo,
  .LearnItem_buttons .btn-remove {
    color: #83b992;
  }
</style>
