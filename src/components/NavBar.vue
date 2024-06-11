<template>
	<nav class="nav">
		<div class="container nav__content">
			<a href="#" class="nav__logo"
				><img src="../assets/images/nike__logo.png" alt="nike"
			/></a>
			<ul class="nav__list">
				<li v-for="(link, i) in links" :key="i">
					<router-link to="/test" href="#" class="nav__list-link">
						{{ link.name }}
					</router-link>
				</li>
			</ul>
			<div class="nav__icons">
				<a href="#" class="nav__icon"
					><img src="../assets/icons/cart.svg" alt="cart"
				/></a>
			</div>
		</div>
	</nav>
</template>

<script setup>
const links = [
	{ name: 'Новинки', to: 'Новинки' },
	{ name: 'Категории', to: 'Категории' },
	{ name: 'Скидки', to: 'Скидки' },
	{ name: 'Продукты ', to: 'Продукты ' },
	{ name: 'О нас', to: 'О нас' },
]
</script>

<style>
.nav {
	padding: 6px 0;
	background: rgb(255, 255, 255);
}

.nav__content {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.nav__list {
	display: flex;

	gap: 71px;
}
.nav__list-link {
	font-family: 'Montserrat';
	color: rgb(0, 0, 0);
	font-size: 16px;
	font-weight: 400;
	line-height: 20px;
}
.nav__icons {
	display: flex;
	
}

</style>
