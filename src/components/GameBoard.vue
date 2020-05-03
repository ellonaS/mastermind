<template>
      <b-form-select  :options="options"></b-form-select>
</template>

<script>
export default {
  name: "game-board",
  data() {
    return {
      options: [
        { value: 1, text: "Red", class: "red" },
        { value: 2, text: "Blue", class: "blue" },
        { value: 3, text: "Yellow", class: "yellow" },
        { value: 4, text: "Green", class: "green" },
        { value: 5, text: "Purple", class: "purple" },
        { value: 6, text: "Gray", class: "gray" }
      ]
    };
  },
};
</script>

<style scoped>
.red {
    background-color: red;
}

</style>