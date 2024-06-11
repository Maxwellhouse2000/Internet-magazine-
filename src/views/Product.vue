<template>
	<div class="container main__section-content">
		<div class="main__section-content-btns">
			<select
				@change="sortItems()"
				v-model="sortBy"
				class="main__section-content-btn-dropdown"
			>
				<option value="sorting">Сортировка</option>
				<option value="price">Цена</option>
				<option value="title">Названия</option>
				<option value="stock">Количество</option>
			</select>
		</div>
		<button class="main__section-content-btn">
			Общее кол-во товаров-{{ items.length }}
		</button>
	</div>
	<section class="product">
		<RouterLink
			:to="`/product/${item.id}`"
			v-for="item in paginatedItems"
			:key="item.id"
			class="container product__content"
		>
			<div class="product__content-item">
				<h4>{{ item.stock }} In stock</h4>
				<img :src="item.thumbnail" alt="" />
				<h1>{{ item.title }}</h1>
				<p>{{ item.description }}</p>
				<div class="product__content-item-info">
					<span>{{ item.price }} $</span>
					<p>{{ item.discountPercentage }} %</p>
				</div>
			</div>
		</RouterLink>
		<div class="product__content-item-pagination">
			<div class="product__content-item-pagination-btn">
				<button :disabled="currentPage === 1" @click="currentPage--">
					<img src="@/assets/icons/left-arrow.svg" alt="" />Прев
				</button>
				<span>{{ currentPage }} / {{ totalPages }}</span>
				<button :disabled="currentPage === totalPages" @click="currentPage++">
					<img src="@/assets/icons/right-arrow.svg" alt="" />След
				</button>
			</div>
		</div>
	</section>
</template>

<script setup>
// import { useProducts } from '@/store/products.js'

import { onMounted, ref, computed } from 'vue'
import axios from 'axios'
const items = ref([])

onMounted(async () => {
	try {
		const { data } = await axios.get('https://dummyjson.com/products?limit=100')
		items.value = data.products
	} catch (err) {
		// console.log(err + "Ошибка при получении товаров")
	}
})
// Текущая страница
const currentPage = ref(1)
const itemsPerPage = 12
const totalPages = computed(() => Math.ceil(items.value.length / itemsPerPage))

const paginatedItems = computed(() => {
	const startIndex = (currentPage.value - 1) * itemsPerPage
	const endIndex = startIndex + itemsPerPage

	return items.value.slice(startIndex, endIndex)
})

// // Отфильтрованные элементы для текущей страницы
// const paginatedItems = computed(() => {
// 	const startIndex = (currentPage.value - 1) * items
// 	const endIndex = startIndex + items
// 	return items.slice(startIndex, endIndex)
// })

const sortBy = ref('sorting')

function sortItems() {
	if (sortBy.value == 'price') {
		items.value.sort((a, b) => {
			const nameA = a.price
			const nameB = b.price
			if (nameA > nameB) return -1
			else 1
		})
	} else if (sortBy.value == 'title') {
		items.value.sort((a, b) => {
			const nameA = a.title.toLowerCase()
			const nameB = b.title.toLowerCase()
			if (nameA > nameB) return -1
			else 1
		})
	} else if (sortBy.value == 'stock') {
		items.value.sort((a, b) => {
			const nameA = a.stock
			const nameB = b.stock
			if (nameA > nameB) return -1
			else 1
		})
	} else {
	}
}

// const products = useProducts()
// products.getProducts()
</script>

<style>
.product__content-item-pagination {
	display: flex;
	align-items: center;
	justify-content: center;
	margin-bottom: 100px;
}
.product__content-item-pagination-btn {
	padding: 5px;
	background: rgb(217, 217, 217);
}

a {
	color: #000;
}
.product {
	margin-top: 100px;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: 20px;
}

.product__content-item {
	padding: 19px 16px;
	width: 306px;
	height: 543px;
	background: rgb(217, 217, 217);
	display: flex;
	flex-direction: column;
	margin-bottom: 100px;
}
.product__content-item h4 {
	background: black;
	color: #ffffff;
	padding: 5px 5px;
	width: 40%;
}
.product__content-item img {
	width: 100%;
	height: 50%;
	object-fit: contain;
}
.product__content-item p {
	margin-top: 32px;
	color: rgb(6, 47, 66);
	font-size: 16px;
	font-weight: 400;
	line-height: 20px;
}
.product__content-item-info {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.product__content-item-info p {
	background: black;
	color: #ffffff;
	padding: 5px 5px;
}
.product__content-item-info button {
	box-sizing: border-box;
	border: 1px solid rgb(0, 92, 103);
	padding: 5px 19px;
}
.product__content-item span {
	margin-top: 20px;
	color: rgb(6, 47, 66);
	font-size: 20px;
	font-weight: 400;
	line-height: 20px;
}
.main__section-content-btns {
	display: flex;
	gap: 100px;
}
.main__section-content-btn {
	background: rgb(255, 255, 255);
	color: rgb(0, 0, 0);
	font-size: 16px;
	font-weight: 400;
	line-height: 20px;
	padding: 12px 12px;
}
.main__section-content-btn-dropdown {
	background: rgb(255, 255, 255);
	color: rgb(0, 0, 0);
	font-size: 16px;
	font-weight: 400;
	line-height: 20px;
	padding: 12px 12px;
}
.main__section-content-btn-dropdown ul {
	margin-top: 12px;
	display: flex;
	align-items: center;
	flex-direction: column;
	gap: 10px;
}
</style>
