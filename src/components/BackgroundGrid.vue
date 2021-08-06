<template>
	<div class="column-1" />
	<div class="column-2" />
	<div class="column-3" />
	<div class="column-hr" />
	<div class="column-hr" />
	<div class="column-hr" />
	<div class="column-hr" />
	<div class="column-hr" />
	<div class="column-hr" />
</template>
<script>
export default {
	name: "BackgroundGrid"
};
</script>
<style>
.column-1 {
	background-color: #151719;
}

.column-2 {
	background-color: #2d2e30;
}

.column-3 {
	background-image: linear-gradient(to right, #4c4a48, #65635e);
}

.column-hr {
	background-color: #a1a3a5;
	border-right: 2px solid #8f8f91;
}
</style>
