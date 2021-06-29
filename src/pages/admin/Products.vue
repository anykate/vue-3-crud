<template>
  <div class="mt-2">
    <h1>Products</h1>
    <table class="table table-sm table-bordered my-4">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Title</th>
          <th scope="col">Image</th>
          <th scope="col">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <th scope="row">{{ product.id }})</th>
          <td>{{ product.title }}</td>
          <td>
            <img
              :src="product.image"
              alt="product.title"
              class="img-fluid"
              width="90"
            />
          </td>
          <td colspan="2">
            <button
              @click="delItem(product.id)"
              class="btn btn-sm btn-danger m-2"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue'
export default {
  name: "Products",
  setup() {
    const products = ref([])
    onMounted(async () => {
      const res = await fetch('http://localhost:3000/products')
      products.value = await res.json()
    })

    const delItem = async (id) => {
      await fetch(`http://localhost:3000/products/${id}`, {
        method: 'GET'
        // method: 'DELETE' - Use this to permanently delete from db
      })
      products.value = products.value.filter(p => p.id !== id);
    }

    return {
      products,
      delItem,
    }
  }
}
</script>

<style scoped>
</style>