<template>
  <div id="app">
    <div>
      <div>{{count}}</div>
      <button v-on:click="handleIncrement">Increment</button>
    </div>
    <div>
      <p>
        <input type="text" v-model="value" />
        <button v-on:click="handleAddItem">Add Item</button>
      </p>
      <ul>
        <li v-for="(item,index) in items" v-bind:key="index">{{item}}</li>
      </ul>
    </div>
    <hr />
    <List />
  </div>
</template>

<script>
import Vue from "vue";
import Vuex from "vuex";
import List from "./components/ListOfItem";
Vue.use(Vuex);
const store = new Vuex.Store({
  state: {
    count: 100,
    items: []
  },
  mutations: {
    increment(state) {
      state.count++;
    },
    addItem(state, value) {
      //state.items = [...state.items, value];
      state.items.push(value);
    }
  },
  actions: {
    increment(context) {
      context.commit("increment");
    },
    addItem(context, value) {
      context.commit("addItem", value);
    }
  }
});

export default {
  name: "app",
  components: {
    List
  },
  store,
  data: function() {
    return {
      value: ""
    };
  },
  computed: {
    count() {
      return this.$store.state.count;
    },
    items() {
      return this.$store.state.items;
    }
  },
  methods: {
    handleIncrement: function() {
      this.$store.dispatch("increment");
    },
    handleAddItem: function() {
      if (this.value) {
        this.$store.dispatch("addItem", this.value);
      } else {
        alert("Error");
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  text-align: center;
  vertical-align: middle;
}
</style>
