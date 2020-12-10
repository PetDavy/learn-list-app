<script>
export default {
  name: 'LearnItem',
  data() {
    return {
      btnRelClassObject: {
        btn: true,
        'btn_add-related': !!this.item.related,
        'btn_creat-related': !this.item.related,
      },
    };
  },
  props: {
    item: Object,
    removeLearn: Function,
  },
};
</script>

<template>
  <li class="LearnItem">
    <span>
      {{item.title}}
    </span>

    <button
      v-if="item.related"
      class="btn btn_related-open"
    >
      related
    </button>

    <button
      :class="btnRelClassObject"
    >
      +
      {{item.related? '': 'add related'}}
    </button>

    <button
      type="button"
      class="btn"
      @click="removeLearn(item.id)"
    >
      REMOVE
    </button>
  </li>
</template>

<style scoped>
  .LearnItem {
    display: flex;
    align-items: center;
  }

  .btn_related-open {
    border: none;
    color: red;
  }

  .btn_add-related {
    padding: 5px 10px;
    font-size: 20px;
    line-height: 20px;
    color: #666;
    border-radius: 50%;
  }

  .btn_creat-related {
    border-radius: 2px;
    background-color: #f4f4f4;
  }
</style>
