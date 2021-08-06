<template>
	<div class="col-schedules off" v-if="session === 'S'">
		<div class="hour">{{ hour }}:{{ minute }}</div>
		<div class="info-off">ESGOTADA</div>
	</div>
	<div class="col-schedules next" v-else-if="isNext === true">
		<div class="hour">{{ hour }}:{{ minute }}</div>
		<div v-if="legend === 'L' && session != 'S'" class="info">LEG</div>
		<div v-else-if="legend === 'D' && session != 'S'" class="info">DUB</div>
		<div v-else-if="legend === 'O' && session != 'S'" class="info">ORI</div>
		<div v-else class="info"></div>
	</div>
	<div class="col-schedules" v-else>
		<div class="hour">{{ hour }}:{{ minute }}</div>
		<div v-if="legend === 'L' && session != 'S'" class="info">LEG</div>
		<div v-else-if="legend === 'D' && session != 'S'" class="info">DUB</div>
		<div v-else-if="legend === 'O' && session != 'S'" class="info">ORI</div>
		<div v-else class="info"></div>
	</div>
</template>

<script>
export default {
	name: "Horario",
	components: {},
	props: {
		hour: String,
		minute: String,
		legend: String,
		session: String,
		isNext: Boolean
	}
};
</script>

<style>
.col-schedules {
	height: 100%;
	width: 100%;
	box-sizing: border-box;

	justify-content: center;
	align-items: center;

	padding-top: 5px;

	font-size: 48px;
	line-height: 50px;
	text-align: center;
	border-right: 2px solid #8f8f91;
}

.off {
	background-color: #be181a;
}

.info-off {
	font-size: 22px;
}

.next {
	background-color: #149911;
}

.info {
	width: 96px;
	height: 29px;
	margin: auto;
	margin-top: 10px;
	background: #a9a9a9;
	border: 1px solid #a0a0a2;
	box-sizing: border-box;
	box-shadow: inset 1px 4px 4px rgba(0, 0, 0, 0.35);
	border-radius: 15px;

	line-height: 26px;
	font-size: 26px;
	text-align: center;
	color: #37383a;
}
</style>
