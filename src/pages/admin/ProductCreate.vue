<template>
  <div class="mt-2">
    <h1>Create Product</h1>
    <form @submit.prevent="addItem">
      <div class="my-4">
        <input
          type="text"
          class="form-control"
          placeholder="Title"
          id="title"
          name="title"
          v-model="title"
        />
        <div class="my-4">
          <input
            type="text"
            class="form-control"
            placeholder="Image URL"
            id="image"
            name="image"
            v-model="image"
          />
        </div>
        <button class="btn btn-outline-primary">Add Product</button>
      </div>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

export default {
  name: "ProductCreate",
  setup() {
    const title = ref('')
    const image = ref('')
    const router = useRouter()

    const addItem = async () => {
      await fetch('http://localhost:3000/products', {
        method: 'POST',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify({
          title: title.value,
          image: image.value
        })
      })
      await router.push('/admin/products')
    }

    return {
      title,
      image,
      addItem,
    }
  }
}
</script>

<style scoped>
</style>