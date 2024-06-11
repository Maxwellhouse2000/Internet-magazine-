<template>
	<section class="main__section">
		<Product />
	</section>
</template>

<script setup>
import Product from '../views/Product.vue'
</script>

<style>
.main__section {
	margin-top: 100px;
}
.main__section-content {
	display: flex;
	align-items: center;
	justify-content: space-between;
}

</style>
