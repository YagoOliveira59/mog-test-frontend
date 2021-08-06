<template>
	<div id="movie-title">
		<div class="col-title">{{ title }}</div>
	</div>
</template>

<script>
export default {
	name: "MovieTitle",
	props: {
		title: String
	}
};
</script>
<style>
#movie-title {
	height: 100%;
	display: block;
	grid-column: 1;

	flex-direction: row;
	flex-wrap: wrap;
	justify-content: center;
	place-items: center;

	padding: 25px;

	font-size: 30px;
	line-height: 30px;
	color: #fff;
	border-bottom: 2px solid #909090 !important;
}

.col-title {
	justify-content: center;
	align-items: stretch;
}
</style>
