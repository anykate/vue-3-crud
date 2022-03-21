<template>
	<div class="mt-2">
		<h1>Products</h1>
		<router-link :to="{ name: 'ProductCreate' }" class="btn btn-outline-primary mt-2">Add Product</router-link>
		<table class="table table-responsive table-sm table-bordered my-4">
			<thead>
				<tr>
					<th scope="col">#</th>
					<th scope="col">Title</th>
					<th scope="col">Image</th>
					<th scope="col" class="text-center">Actions</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="product in products" :key="product.id">
					<th scope="row">{{ product.id }})</th>
					<td>{{ product.title }}</td>
					<td>
						<img :src="product.image" :alt="product.title" class="img-fluid" width="90" />
					</td>
					<td class="align-middle">
						<div class="container">
							<div class="row">
								<div class="col-md-6">
									<router-link :to="{ name: 'ProductEdit', params: { id: product.id } }" class="h5">
										<i class="bi bi-pencil"></i>
									</router-link>
								</div>
								<div class="col-md-6">
									<button
										type="button"
										@click="delItem(product.id)"
										class="border-0 bg-transparent p-0 h5 text-danger"
									>
										<i class="bi bi-x-circle"></i>
									</button>
								</div>
							</div>
						</div>
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
			const res = await fetch('http://localhost:3004/products')
			products.value = await res.json()
		})

		const delItem = async (id) => {
			await fetch(`http://localhost:3004/products/${id}`, {
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