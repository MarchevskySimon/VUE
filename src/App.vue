<template>
  <h1>Nova polozka</h1>

  <label for="">Nazov polozky</label>
  <br />
  <input v-model="input" placeholder="Meno" />
  <br />
  <button @click="addItem()">Pridat</button>
  <hr />

  <h2>Polozky</h2>
  <ul>
    <li v-for="item in validItems" :key="item.id">
      <span @click="deleteItem(item)" style="margin-right: 15px">X</span>
      {{ item.text }}
    </li>
  </ul>
  <hr />

  <!-- DELETED -->

  <h2>Zmazane polozky</h2>
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
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
body {
  padding: 3rem;
  background-color: black;
}
h1,
h2,
p,
label,
li {
  color: white;
}
</style>
