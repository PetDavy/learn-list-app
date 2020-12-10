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
      this.addNewLearn(this.inputValue);
      this.inputValue = '';
    },
  },
};
</script>

<template>
  <form @submit.prevent="add">
    <input
      type="text"
      v-model="inputValue"
    >
    <button type="submit">
      Add to Learn
    </button>
  </form>
</template>
