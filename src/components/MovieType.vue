<template>
	<div id="type">
		<div class="col-type" v-if="chair === 'VP'">
			<div class="premierM">PREMIER</div>
		</div>
		<div class="col-type" v-else>
			<div v-if="type === 'NO'">2D</div>
			<div v-else-if="type === 'XD'" class="XD">XD</div>
			<div v-else>3D</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "MovieType",
	props: {
		type: String,
		chair: String
	}
};
</script>

<style>
#type {
	grid-column: 3;
	display: block;
	box-sizing: border-box;

	flex-direction: row;
	flex-wrap: wrap;
	place-items: center;
	border-bottom: 2px solid #909090 !important;
}

.col-type {
	padding: 15px 0;
	place-items: center;
	align-items: stretch;

	font-family: "Raleway", sans-serif !important;
	font-size: 60px;
	line-height: 60px;
	text-align: center;
	color: #686866;
	text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.4), 3px -4px 4px rgba(0, 0, 0, 0.2);
}

.col-type .XD {
	font-family: "Raleway", sans-serif !important;
	font-size: 60px;
	line-height: 60px;
	text-align: center;
	color: #f4f4f2;
	text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25), 3px 0px 3px rgba(236, 41, 34, 0.513);
}

.col-type .premierM {
	font-family: "Raleway", sans-serif !important;
	font-size: 28px;
	line-height: 60px;
	text-align: center;
	color: #fced9e;
}
</style>
