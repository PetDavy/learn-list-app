<script>
import Header from './components/Header.vue';
import LearnList from './components/LearnList.vue';
import AddLearnItem from './components/AddLearnItem.vue';

export default {
  name: 'App',
  components: {
    Header,
    AddLearnItem,
    LearnList,
  },
  data() {
    return {
      learnList: [],
      lastIndex: 0,
    };
  },
  methods: {
    addNewLearn(newItem) {
      const newLearn = {
        id: this.lastIndex,
        title: newItem,
      };

      this.learnList = [newLearn, ...this.learnList];
      this.lastIndex += 1;
      this.save();
    },
    removeLearn(id) {
      this.learnList = this.learnList.filter((item) => item.id !== id);
      this.save();
    },
    save() {
      // localStorage.setItem('learnList', JSON.stringify(this.learnList));
    },
  },
  mounted() {
    const savedList = localStorage.getItem('learnList');

    if (savedList) {
      this.learnList = JSON.parse(savedList);
      console.log(savedList);
    }
  },
};
</script>

<template>
  <Header />
  <AddLearnItem
    :addNewLearn="addNewLearn"
  />
  <LearnList
    :learnList="learnList"
    :removeLearn="removeLearn"
  />
</template>

<style>
#app {
  padding: 20px 60px;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body,
h1,
h2,
h3,
p,
ul,
li {
  margin: 0;
  padding: 0;
}

.btn {
  padding: 5px 15px;
  margin: 0 5px;
  border: 1px solid #ccc;
  background-color: inherit;
  color: blue;

  cursor: pointer;
}
</style>
