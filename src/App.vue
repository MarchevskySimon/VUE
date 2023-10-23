<template>
  <input v-model="input" />
  <button @click="addItem()">Add to list</button>

  <h2>Polozky</h2>
  <ul>
    <li v-for="item in validItems" :key="item.id">
      <span @click="deleteItem(item)" style="margin-right: 15px">X</span>
      {{ item.text }}
    </li>
  </ul>

  <!-- DELETED -->

  <ul class="delete-ul">
    <li v-for="item in deletedItems" :key="item.id">
      <span @click="deleteItem(item)" style="margin-right: 15px">X</span>
      <s>
        {{ item.text }}
      </s>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      list: [],
    };
  },

  computed: {
    validItems() {
      return this.list.filter((item) => !item.is_deleted);
    },

    deletedItems() {
      return this.list.filter((item) => item.is_deleted);
    },
  },

  methods: {
    addItem() {
      this.list.push({
        id: this.list.length + 1,
        text: this.input,
        is_deleted: false,
      });
      this.input = "";
    },
    deleteItem(item) {
      item.is_deleted = true;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  list-style: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

.delete-ul {
  margin-top: 3rem;
  padding: 3rem;
  border-top: 2px solid black;
}
</style>
