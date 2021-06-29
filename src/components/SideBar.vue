<template>
  <div class="sidebar">
    <ul class="navbar-nav p-3">
      <li><router-link :to="{ name: 'Products' }">Products</router-link></li>
      <li>
        <router-link :to="{ name: 'ProductCreate' }">Add Product</router-link>
      </li>
      <li>
        <router-link :to="{ name: 'ProductEdit', params: { id: 3 } }"
          >Edit Product</router-link
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
}
</script>

<style scoped>
</style>