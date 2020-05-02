<template>
      <b-form-select v-model="selected" :options="options"></b-form-select>
</template>

<script>
export default {
  name: "game-board",
  data() {
    return {
      selected: [],
      options: [
        { value: 1, text: "Red" },
        { value: 2, text: "Blue" },
        { value: 3, text: "Yellow" },
        { value: 4, text: "Green" },
        { value: 5, text: "Purple" },
        { value: 6, text: "Gray" }
      ]
    };
  },
};
</script>

<style scoped>
.Red {
    background-color: red;
}

</style>