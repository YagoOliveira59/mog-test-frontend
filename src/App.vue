<template>
	<div class="background-grid">
		<BackgroundGrid />
	</div>
	<div>
		<transition name="component-fade" mode="out-in">
			<FeaturedGrid v-show="updated" />
		</transition>
	</div>
</template>

<script>
import FeaturedGrid from "./components/FeaturedGrid.vue";
import BackgroundGrid from "./components/BackgroundGrid.vue";

export default {
	name: "App",
	components: {
		FeaturedGrid,
		BackgroundGrid
	},
	data() {
		return {
			seconds: 0,
			updated: true
		};
	},
	watch: {
		seconds: function() {
			if (this.seconds === 0) {
				this.updated = false;
			} else {
				this.updated = true;
			}
		}
	},
	beforeCreate() {
		setInterval(() => {
			const GET_DATE = new Date();
			this.seconds = GET_DATE.getSeconds();
		}, 1000);
	}
};
</script>
<style>
.component-fade-enter-active,
.component-fade-leave-active {
	transition: all 0.3s ease-out;
}

.component-fade-enter-from,
.component-fade-leave-to {
	opacity: 0;
}

.background-grid {
	display: grid;
	grid-template-columns: 455px 94px 141px repeat(6, 205px);
	grid-template-rows: 900px;
	grid-auto-flow: row;
	z-index: 0;
}
</style>
