import { onMounted, ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'
<template>
	<div class="mt-2">
		<h1>Edit Product</h1>
		<form @submit.prevent="editItem">
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
				<button class="btn btn-outline-primary">Save</button>
			</div>
		</form>
	</div>
</template>

<script>
import { onMounted, ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'

export default {
  name: "ProductEdit",
  props: {
    id: {
      Number
    }
  },
  setup() {
    const title = ref('')
    const image = ref('')
    const router = useRouter()
    const route = useRoute()

    onMounted(async () => {
      const res = await fetch(`http://localhost:3004/products/${route.params.id}`);
      const product = await res.json();
      title.value = product.title;
      image.value = product.image;
    })

    const editItem = async () => {
      await fetch(`http://localhost:3004/products/${route.params.id}`, {
        method: 'PUT',
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
      editItem,
    }
  }
}
</script>

<style scoped>
</style>