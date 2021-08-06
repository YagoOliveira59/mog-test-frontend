<template>
	<div class="col-classify">
		<div v-if="classInd === '0'" class="icon livre">L</div>
		<div v-else-if="classInd === '10'" class="icon dez">{{ classInd }}</div>
		<div v-else-if="classInd === '12'" class="icon doze">{{ classInd }}</div>
		<div v-else-if="classInd === '14'" class="icon catorze">{{ classInd }}</div>
		<div v-else class="icon dezesseis">{{ classInd }}</div>
	</div>
</template>

<script>
export default {
	name: "MovieClass",
	props: {
		classInd: String
	}
};
</script>
<style>
.col-classify {
	grid-column: 2;
	display: block;
	box-sizing: border-box;

	padding: 16px;
	line-height: 50px;
	border-bottom: 2px solid #909090 !important;
}

.icon {
	width: 64px;
	height: 64px;

	box-sizing: border-box;
	box-shadow: 1px 4px 4px rgba(0, 0, 0, 0.7);
	border-radius: 5px;
	margin: auto;
	padding: 5px;

	font-size: 40px;
	text-align: center;
	color: #fff;
	text-shadow: 0px 2px 2px rgba(0, 0, 0, 0.4);
}

.livre {
	background: #00a926;
	border: 1px solid #0a8a2d;
}

.dez {
	background: #0080e1;
	border: 1px solid #0f6cb2;
}

.doze {
	background: #f3b001;
	border: 1px solid #c2900d;
}

.catorze {
	background: #ff7201;
	border: 1px solid #c96717;
}

.dezesseis {
	background: #de2824;
	border: 1px solid #b71417;
}
</style>
