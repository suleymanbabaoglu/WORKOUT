<template>
  <b-sidebar
    :bg-variant="variant"
    shadow
    visible
    no-close-on-route-change
    no-header-close
    no-close-on-esc
    no-close-on-backdrop
  >
    <template #title>
      <b-img
        src="https://avatars1.githubusercontent.com/u/22965283?s=100&v=4"
      />
      <span class="text-white">BVC</span>
    </template>
    <b-dd-divider style="margin-top: -30px"></b-dd-divider>

    <b-navbar-nav class="pl-3">
      <b-nav-item to="/" active><b-icon-house /> Dashboard</b-nav-item>
      <b-nav-item to="customer"><b-icon-basket /> Customer</b-nav-item>
      <b-nav-item to="user"><b-icon-person /> User</b-nav-item>
      <b-nav-item to="product"><b-icon-display /> Product</b-nav-item>
      <b-nav-item to="settings"><b-icon-gear /> Settings</b-nav-item>
    </b-navbar-nav>
  </b-sidebar>
</template>
<script>
export default {
  props: ["variant"],
};
</script>
<style>
.b-sidebar {
  width: 200px !important;
}
.nav-link {
  color: #fff;
}
.nav-link:hover {
  font-weight: bold;
  color: #563d7c;
  background-color: #41b883;
}
</style>
