<template>
      <b-form-select v-model="selected" :options="options"></b-form-select>
</template>

<script>
export default {
  name: "game-board",
  data() {
    return {
      gameComplexity: 4,
      selected: [],
      options: [
        { value: null, text: "select", disabled: true },
        { value: "1", text: "Red" },
        { value: "2", text: "Blue" },
        { value: "3", text: "Yellow" },
        { value: "4", text: "Green" },
        { value: "5", text: "Purple" },
        { value: "5", text: "grey" }
      ]
    };
  },
  methods: {
    selectionMade() {
      this.selection = document.getElementById("search").value;
      this.$emit("filter-tools", this.query);
    }
  }
};
</script>

<style scoped>
</style>