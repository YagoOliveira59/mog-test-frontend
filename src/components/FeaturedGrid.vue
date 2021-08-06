<template>
	<div class="container">
		<template v-for="value in items" :key="value.id">
			<GridItem
				v-if="value.schedules.length > 0 && value.id != ''"
				v-bind:title="value.title"
				v-bind:classInd="value.classInd"
				v-bind:type="value.type"
				v-bind:chair="value.chair"
				v-bind:schedules="value.schedules"
			/>
		</template>
	</div>
</template>

<script>
import BackgroundGrid from "./BackgroundGrid.vue";
import GridItem from "./GridItem.vue";

import featuredGridData from "../data/GRADE_DESTAQUE_688.txt";

export default {
	name: "FeaturedGrid",
	components: {
		BackgroundGrid,
		GridItem
	},
	data() {
		return {
			items: [],
			interval: 0
		};
	},
	watch: {
		interval(val) {
			if (val === 1) return this.handleUpdateMovies();
		}
	},
	beforeCreate() {
		setInterval(() => {
			const GET_DATE = new Date();
			const GET_SECUND = GET_DATE.getSeconds();
			this.interval = GET_SECUND;
		}, 1000);
	},
	created() {
		this.handleCreateDataBase();
	},
	beforeMount() {
		this.handleCreateMovie();
		this.handleCreateSchedules();
	},
	mounted() {
		this.handleUpdateMovies();
	},
	methods: {
		handleCreateDataBase() {
			const DATABASE_MOVIE = featuredGridData.split("\n");
			return DATABASE_MOVIE;
		},
		handleSetIndexSubstring() {
			// set substring index
			const INDEX_ID = { start: 2, end: 10 };
			const INDEX_HOUR = { start: 10, end: 12 };
			const INDEX_MINUTE = { start: 13, end: 15 };
			const INDEX_TITLE = { start: 15, end: 75 };
			const INDEX_CLASS = { start: 75, end: 77 };
			const INDEX_LEGEND = { start: 80, end: 81 };
			const INDEX_SESSION = { start: 81, end: 82 };
			const INDEX_TYPE = { start: 91, end: 93 };
			const INDEX_CHAIR = { start: 174, end: 176 };

			return {
				INDEX_ID,
				INDEX_HOUR,
				INDEX_MINUTE,
				INDEX_TITLE,
				INDEX_CLASS,
				INDEX_LEGEND,
				INDEX_SESSION,
				INDEX_TYPE,
				INDEX_CHAIR
			};
		},
		handleCreateMovie() {
			const MOVIES_LIST = [];
			const INDEX = this.handleSetIndexSubstring();
			const DATABASE_MOVIE = this.handleCreateDataBase();

			class Movie {
				constructor(id, title, classInd, type, chair, schedules) {
					this.id = id;
					this.title = title;
					this.classInd = classInd;
					this.type = type;
					this.chair = chair;
					this.schedules = schedules;
				}
			}

			function createMovie(movie) {
				const MOVIE_ID = movie.substring(INDEX.INDEX_ID.start, INDEX.INDEX_ID.end);
				const MOVIE_TITLE = movie.substring(INDEX.INDEX_TITLE.start, INDEX.INDEX_TITLE.end).trim();
				const MOVIE_CLASS = movie.substring(INDEX.INDEX_CLASS.start, INDEX.INDEX_CLASS.end).trim();
				const MOVIE_TYPE = movie.substring(INDEX.INDEX_TYPE.start, INDEX.INDEX_TYPE.end);
				const MOVIE_CHAIR = movie.substring(INDEX.INDEX_CHAIR.start, INDEX.INDEX_CHAIR.end);
				const MOVIE = new Movie(MOVIE_ID, MOVIE_TITLE, MOVIE_CLASS, MOVIE_TYPE, MOVIE_CHAIR);
				if (MOVIES_LIST.length > 0) {
					var movieAdd = false;
					MOVIES_LIST.forEach(list => {
						if (list.id === MOVIE_ID && list.type === MOVIE_TYPE && list.chair === MOVIE_CHAIR)
							return (movieAdd = true);
					});
					if (!movieAdd) return MOVIES_LIST.push(MOVIE);
				} else {
					return MOVIES_LIST.push(MOVIE);
				}
				return;
			}

			DATABASE_MOVIE.forEach(createMovie);

			return MOVIES_LIST;
		},
		handleCreateSchedules() {
			const MOVIES_LIST = this.handleCreateMovie();
			const INDEX = this.handleSetIndexSubstring();
			const DATABASE_MOVIE = this.handleCreateDataBase();

			class Schedules {
				constructor(hour, minute, legend, session, isNext) {
					this.hour = hour;
					this.minute = minute;
					this.legend = legend;
					this.session = session;
					this.isNext = isNext;
				}
			}

			function createSchedules() {
				MOVIES_LIST.forEach(item => {
					const NEW_SCHEDULE = [];
					DATABASE_MOVIE.forEach(movie => {
						const GET_ID = movie.substring(INDEX.INDEX_ID.start, INDEX.INDEX_ID.end).trim();
						const GET_TYPE = movie.substring(INDEX.INDEX_TYPE.start, INDEX.INDEX_TYPE.end);
						const GET_CHAIR = movie.substring(INDEX.INDEX_CHAIR.start, INDEX.INDEX_CHAIR.end);
						const MOVIE_HOUR = movie.substring(INDEX.INDEX_HOUR.start, INDEX.INDEX_HOUR.end);
						const MOVIE_MINUTE = movie.substring(INDEX.INDEX_MINUTE.start, INDEX.INDEX_MINUTE.end);
						const MOVIE_LEGEND = movie.substring(INDEX.INDEX_LEGEND.start, INDEX.INDEX_LEGEND.end);
						const MOVIE_SESSION = movie.substring(
							INDEX.INDEX_SESSION.start,
							INDEX.INDEX_SESSION.end
						);
						const MOVIE_START = false;
						const SCHEDULE = new Schedules(
							MOVIE_HOUR,
							MOVIE_MINUTE,
							MOVIE_LEGEND,
							MOVIE_SESSION,
							MOVIE_START
						);
						if (item.id === GET_ID && item.type === GET_TYPE && item.chair === GET_CHAIR)
							return NEW_SCHEDULE.push(SCHEDULE);
					});
					NEW_SCHEDULE.sort(compare);
					item.schedules = NEW_SCHEDULE;
				});
			}

			function compare(a, b) {
				if (a.hour === b.hour) {
					if (a.minute < b.minute) return -1;
					if (a.minute > b.minute) return 1;
					return 0;
				}
				if (a.hour < b.hour) return -1;
				if (a.hour > b.hour) return 1;
				return 0;
			}
			MOVIES_LIST.forEach(createSchedules);
			return (this.items = MOVIES_LIST);
		},
		handleUpdateMovies() {
			const DATE = new Date();
			const NOW_HOUR = DATE.getHours();
			const NOW_MINUTE = ("0" + DATE.getMinutes()).slice(-2);

			function updateMoviesList(value) {
				const M_INDEX = value.schedules;
				const MOVIE_SCHEDULES = [];
				M_INDEX.forEach(item => {
					const AUX_MOVIE_HOUR = parseInt(item.hour);
					const AUX_MOVIE_MINUTE = parseInt(item.minute);

					if (AUX_MOVIE_HOUR < 6) return;
					if (AUX_MOVIE_HOUR < NOW_HOUR) return;
					else {
						if (AUX_MOVIE_HOUR === NOW_HOUR) {
							if (AUX_MOVIE_MINUTE < NOW_MINUTE) return;
							else {
								let difference = Math.abs(NOW_MINUTE - AUX_MOVIE_MINUTE);
								if (difference <= 15) {
									item.isNext = true;
								}
								return MOVIE_SCHEDULES.push(item);
							}
						} else return MOVIE_SCHEDULES.push(item);
					}
				});
				return (value.schedules = MOVIE_SCHEDULES);
			}
			return this.items.filter(updateMoviesList);
		}
	}
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	border: 0;
	box-sizing: border-box;
}

.container {
	position: absolute;
	top: 0;
	left: 0;
	display: grid;
	grid-template-columns: 455px 94px 141px repeat(6, 205px);
	grid-template-rows: repeat(7, 106px);
	grid-auto-flow: row;
	z-index: 1;
	color: #fff;

	font-family: "Poppins", sans-serif;
	font-weight: 600;
	text-transform: uppercase;
	font-feature-settings: "pnum" on, "lnum" on;
}
</style>
