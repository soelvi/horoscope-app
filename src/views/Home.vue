<template>
	<main class="horoscope">
		<h2 class="horoscope__header"> 
		{{ title }}
		</h2>
	
		<h1 class="horoscope__title"> 
				<img src="/public/images/moonstars.png" alt="" class="horoscope__icon">
					{{ name }} 
				<img src="/public/images/stars.png" alt="" class="horoscope__icon">
		</h1>

		<h1 class="horoscope__title"> your sign </h1>
		<span class="horoscope__sign">
			<select v-model="currentSign">
				<option v-for="sign in allSigns" :value="sign" :key="sign"> {{ sign }} </option>
			</select>
			<button @click="fetchData">enter sign</button> 
		</span>

		<span class="horoscope__days">
			<button @click="getYesterday"> <svg width="20" height="20" viewBox="0 0 20 29" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M0.31559 14.7281L17.8498 0.294584L18.3964 28.4706L0.31559 14.7281Z" fill="#D0E1F9"/> </svg> </button>
			<h1 class="horoscope__daysTitle"> {{ currentDate }} </h1>	
			<button @click="getTomorrow"> <svg width="20" height="20" viewBox="0 0 20 29" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M19.0916 14.7765L0.982376 28.4816L1.58729 0.306788L19.0916 14.7765Z" fill="#D0E1F9"/> </svg> </button>
		</span>

		<p class="horoscope_currentDate"> {{ horoscope.current_date }} </p>
		<p class="horoscope_description"> {{ horoscope.description }} </p>

		<h1 class="horoscope__title"> lucky number </h1>
		<span class="horoscope__luckyNumber"> {{ horoscope.lucky_number }} </span>
	</main>
</template>

<script>

export default {
	data() {
		return {
			title: 'read your daily horoscope',
			name: 'ASTROWORLD',
			horoscope: {},
			currentSign: 'aries',
			allSigns: [
				"aries", "taurus", "gemini", "cancer", "leo", "virgo", "libra", "scorpio", "sagittarius", "capricorn", "aquarius", "pisces"
			],
			currentDate: 'today',
			allDates: [ "yesterday", "today", "tomorrow" ]
		}
	},

	created() {
		this.fetchData();
	},

	methods: {
		async fetchData() {
			const url = `https://aztro.sameerkumar.website/?sign=${this.currentSign}&day=${this.currentDate}`; // lage literal string 
			const options = {method: 'POST'}
			const response = await fetch(url, options); // default as GET 
			const results = await response.json();
			this.horoscope = results;
		},

		getYesterday(){
			console.log('clicked yesterday')
		},

		getTomorrow(){
			console.log('clicked tomorrow')
		},
	}
}
</script>

<style>

button {
	color: #efb509;
	padding: 10px;
}

select {
	padding: 5px;
	font-size: var(--font-size);
	font-family: var(--font-family);
	color: var(--background);
	border-radius: 20px;
	text-align: center;
	background-color: #efb509;
	opacity: 80%;
	border-style: none;
}

.horoscope {
	padding: 50px;
	margin: 2%;
	/* background: var(--background); */
	height: 100vh;	
	display: flex;
	flex-direction: column;
	justify-content:space-evenly;
	text-align: center;
}

.horoscope__header {
	color: #efb509;
	padding-bottom: var(--padding-bottom);
}

.horoscope__title {
	color: var(--title-color);
	font-size: var(--font-size-title);
	padding-bottom: var(--padding-bottom);
}

.horoscope__icon {
	width: 50px;
	height: 50px;
}

.horoscope__daysTitle {
	color: var(--title-color);
	font-size: var(--font-size-title);
}

.horoscope__sign {
	padding-bottom: var(--padding-bottom);
}

.horoscope__days {
	display: flex;
	justify-content: center;
	padding-bottom: var(--padding-bottom);
}

.horoscope_description {
	color: var(--title-color);
	font-size: var(--font-size);
	width: 400px;
	align-self: center;
	line-height: var(--line-height);
	padding-bottom: var(--padding-bottom);
}

.horoscope_currentDate {
	color: var(--title-color);
	padding-bottom: var(--padding-bottom);
}

.horoscope__luckyNumber {
	display: flex;
	flex-direction: column;
	justify-content: center;
	width: 55px;
	height: 55px;
	background-color: #efb509;
	opacity: 80%;
	border-radius: 50px;
	font-size: 24pt;
	color: var(--background);
	align-self: center;
}

/* 800px tablet and smaller -- mobile */
	@media screen and (max-width: 800px) { 
		.horoscope__header {
			padding-bottom: var(--padding-bottom-small);
		}

		.horoscope__title {
			font-size: var(--font-size-smaller);
		}

		.horoscope__icon {
			width: 25px;
			height: 25px;
		}

		.horoscope__daysTitle {
			font-size: var(--font-size-smaller);
		}	

		.horoscope__sign {
			padding-bottom: var(--padding-bottom-small);
		}

		.horoscope__days {
			display: flex;
			justify-content: center;
			padding-bottom: var(--padding-bottom-small);
		}

		.horoscope_description {
			padding-bottom: var(--padding-bottom-small);
		}

		.horoscope_currentDate {
			padding-bottom: var(--padding-bottom-small);
		}
}
</style>

