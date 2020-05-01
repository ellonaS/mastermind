<template>
  <div>
    <b-navbar toggleable="md" type="dark" variant="info" id="navbar">
      <b-navbar-brand :to="{name: 'Home'}">
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item :to="{name: 'Home'}">WHAT we do</b-nav-item>
          <b-nav-item :to="{name: 'Home'}">WHO we are</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "game-header"
};
</script>

<style scoped>
#navbar {
  padding-left: 5%;
  padding-right: 5%;
}
img {
  width:20%;
}
</style>