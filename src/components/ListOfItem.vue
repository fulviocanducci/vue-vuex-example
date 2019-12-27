<template>
  <div id="list">
    <ul>
      <li v-for="(item,index) in items" v-bind:key="index">{{item}}</li>
    </ul>
    {{count}}
  </div>
</template>

<script>
export default {
  name: "list",
  computed: {
    count() {
      return this.$store.state.count;
    },
    items() {
      return this.$store.state.items;
    }
  }
};
</script>