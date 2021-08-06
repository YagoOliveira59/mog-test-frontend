<template>
	<div id="item">
		<MovieTitle
			v-bind:title="title"
			:class="[schedules.length > 6 ? 'duplo' : '', chair === 'VP' ? 'premier' : '']"
		/>
		<MovieClass v-bind:classInd="classInd" :class="[schedules.length > 6 ? 'duplo' : '']" />
		<MovieType
			v-bind:type="type"
			v-bind:chair="chair"
			:class="[schedules.length > 6 ? 'duplo' : '']"
		/>
		<div class="grid-schedules" :class="[schedules.length > 6 ? 'duplo' : '']">
			<div
				class="row-schedules"
				:class="[schedules.length > 6 ? 'duplo' : '', chair === 'VP' ? 'premier' : '']"
			>
				<MovieSchedules
					v-for="(value, index) in schedules"
					:key="index"
					v-bind:hour="value.hour"
					v-bind:minute="value.minute"
					v-bind:legend="value.legend"
					v-bind:session="value.session"
					v-bind:isNext="value.isNext"
				/>
			</div>
		</div>
	</div>
</template>

<script>
import MovieTitle from "./MovieTitle.vue";
import MovieClass from "./MovieClass.vue";
import MovieSchedules from "./MovieSchedules.vue";
import MovieType from "./MovieType.vue";

export default {
	name: "GridItem",
	components: {
		MovieTitle,
		MovieClass,
		MovieSchedules,
		MovieType
	},
	props: {
		title: String,
		classInd: String,
		schedules: Array,
		type: String,
		chair: String
	}
};
</script>

<style>
#item {
	display: contents;
	flex-direction: row;
	box-sizing: border-box;
	position: absolute;
	top: 0;
	z-index: 1;
}

.duplo {
	grid-row: span 2;
	place-items: center;
}

.premier {
	background-color: #28241c;
	color: #c6b7a3;
}

.grid-schedules {
	grid-column: 4 !important;
	display: block;
	align-content: flex-start;
	flex-direction: row;

	color: #343434;
}

.row-schedules {
	grid-template-columns: repeat(6, 205px);
	grid-template-rows: 104px;
	height: 100%;
	display: inline-grid;
	box-sizing: border-box;
	border-bottom: 2px solid #909090 !important;
}
</style>
