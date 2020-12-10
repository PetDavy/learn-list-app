<script>
import LearnItem from './LearnItem.vue';

export default {
  name: 'LearnList',
  components: {
    LearnItem,
  },
  props: {
    learnList: Array,
    removeLearn: Function,
  },
};
</script>

<template>
  <h3 v-if="!learnList.length">There is nothing to learn</h3>

  <ul
    class="LearnList"
    v-if="learnList.length"
  >
    <LearnItem
      v-for="item in learnList"
      :key="item.id"
      :item="item"
      :removeLearn="removeLearn"
    />
  </ul>
</template>

<style scoped>
  .LearnList {
    list-style: none;
    padding: 10px 20px;
    border: 1px solid #ccc;
  }
</style>
