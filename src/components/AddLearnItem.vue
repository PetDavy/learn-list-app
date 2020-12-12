<script>
export default {
  name: 'AddLearnItem',
  data() {
    return {
      inputValue: '',
    };
  },
  props: {
    addNewLearn: Function,
  },
  methods: {
    add() {
      if (!this.inputValue) {
        return;
      }

      this.addNewLearn(this.inputValue);
      this.inputValue = '';
    },
  },
};
</script>

<template>
  <form
    @submit.prevent="add"
    class="add-learn-item"
  >
    <input
      type="text"
      v-model="inputValue"
      class="add-learn-input"
      placeholder="Add subject to learn..."
    >
    <button
      type="submit"
      class="btn add-learn-btn"
    >
      +
    </button>
  </form>
</template>

<style scoped>
  .add-learn-item {
    display: flex;
    padding: 10px;
    margin-bottom: 15px;

    border-radius: 5px;
    height: 60px;
    background-color: #83B992;
    color: #f4f4f4;
  }

  .add-learn-input {
    padding-left: 15px;
    flex-grow: 1;
    background-color: inherit;
    border: none;
    color: inherit;
    outline: none;
    font-size: 20px;
  }

  .add-learn-input::placeholder {
    color: #e6e6e6;
  }

  .add-learn-btn {
    height: 40px;
    width: 40px;
    border: none;
    background-color: transparent;
    border-radius: 50%;
    color: inherit;
    font-size: 30px;

    transition: transform 0.3s;
  }

  .add-learn-btn:hover {
    transform: scale(1.03);
    background-color: rgba(255, 255, 255, 0.2);
  }
</style>
