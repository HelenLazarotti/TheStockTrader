<template>
	<v-app>
		<Header />
		<v-content>
			<v-container>
				<transition name="slide" mode="out-in">
					<router-view></router-view>
				</transition>
			</v-container>
		</v-content>	
		<Footer />
	</v-app>



</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer.vue';

export default {
	components: { Header, Footer },
	created() {
		this.$store.dispatch('initStocks')
	}
}
</script>

<style>
	#app{
		background-color: #636363;
		color: #fff;
	}
	@keyframes slide-in {
		from { transform: translateY(-30px); opacity: 0; }
		to { transform: translateY(0px); opacity: 1; }
	}

	@keyframes slide-out {
		from { transform: translateY(0px); opacity: 1; }
		to { transform: translateY(-30px); opacity: 0; }
	}

	.slide-enter-active {
		animation: slide-in 0.3s ease;
	}

	.slide-leave-active {
		animation: slide-out 0.3s ease;
	}
</style>

