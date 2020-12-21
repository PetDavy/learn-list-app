<script>
import Header from './components/Header.vue';
import LearnList from './components/LearnList.vue';
import AddLearnItem from './components/AddLearnItem.vue';
import Notes from './components/Notes.vue';
import RelatedInfo from './components/RelatedInfo.vue';

export default {
  name: 'App',
  components: {
    Header,
    AddLearnItem,
    LearnList,
    Notes,
    RelatedInfo,
  },
  data() {
    return {
      learnList: [],
      lastIndex: 0,
      selectedItem: null,
      isNotesOpen: false,
      isInfoOpen: false,
    };
  },
  methods: {
    addNewLearn(newItem) {
      const newLearn = {
        id: this.lastIndex + 1,
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
      localStorage.setItem('learnList', JSON.stringify(this.learnList));
      localStorage.setItem('lastIndex', this.lastIndex);
    },
    openNotes(id) {
      this.selectedItem = this.learnList.find((item) => item.id === id);
      this.isNotesOpen = true;
    },
    openInfo(id) {
      this.selectedItem = this.learnList.find((item) => item.id === id);
      this.isInfoOpen = true;
    },
    closeModal(updatedItem = null) {
      this.selectedItem = null;
      this.isInfoOpen = false;
      this.isNotesOpen = false;

      if (!updatedItem) {
        return;
      }

      this.learnList = this.learnList.map((item) => {
        if (item.id !== updatedItem.id) {
          return item;
        }

        return updatedItem;
      });

      this.save();
    },
  },
  mounted() {
    const savedList = localStorage.getItem('learnList');
    const lastIndex = localStorage.getItem('lastIndex');

    if (savedList) {
      this.learnList = JSON.parse(savedList);
    }

    if (lastIndex) {
      this.lastIndex = lastIndex;
    }
  },
};
</script>

<template>
  <Header />
  <main class="main">
    <AddLearnItem
      @add-new-learn="addNewLearn"
    />
    <LearnList
      :removeLearn="removeLearn"
      :learnList="learnList"
      :openNotes="openNotes"
      :openInfo="openInfo"
    />

    <Notes
      v-if="isNotesOpen"
      :selectedItem="selectedItem"
      @close-modal="closeModal"
    />

    <RelatedInfo
      v-if="isInfoOpen"
      :selectedItem="selectedItem"
      @close-modal="closeModal"
    />
  </main>
</template>

<style>
#app {
  font-family: 'Poppins', sans-serif;
  color: #2c3e50;
  min-height: 100vh;
  background: linear-gradient(90deg, rgba(151,204,169,1) 35%, rgba(249,228,163,1) 100%);
}

.main {
  max-width: 1000px;
  margin: 0 auto;
}

*,
*::before,
*::after {
  box-sizing: border-box;
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
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 5px 15px;
  margin: 0 5px;
  border: 1px solid #ccc;
  background-color: inherit;
  color: blue;

  cursor: pointer;
}

.btn-close-modal {
  position: fixed;
  top: 20px;
  right: 20px;
  color: #f4f4f4;
  font-size: 32px;
  font-weight: 500;
  border: none;
  background-color: transparent;
}
</style>
