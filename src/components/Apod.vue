<template>
	<div id="container">
		<h3>NASA | Astronomy Picture of the Day</h3>
		<br />
		<p>Select a date:</p>
		<input type="date" data-date-inline-picker="true" v-model="dateFromField" />
		&nbsp; <button @click="getPhoto">get photo</button> <br /><br />
		<div id="error">
			{{ error ? `That day hasn't happened yet! ${error}` : null }}
			<p></p>
		</div>

		<h3 id="title">{{ title }}</h3>
		<img :src="src" alt="" />
		<iframe :src="src" width="530" height="300" v-if="isVideo"></iframe>
		<p id="explanation">{{ explanation }}</p>
		<p>{{ copyright ? `Credit to ${copyright}` : null }}</p>
	</div>
</template>

<script>
import moment from "moment";

export default {
	data() {
		return {
			url: process.env.VUE_APP_URL,
			uri: process.env.VUE_APP_URI,
			dateFromField: "",
			title: "",
			src: "",
			explanation: "",
			copyright: "",
			isVideo: false,
			error: "",
		};
	},
	mounted() {
		fetch(this.uri)
			.then((res) => res.json())
			.then((data) => {
				console.log(data);
				this.title = data.title;
				this.src = data.url;
				this.explanation = data.explanation;
				this.copyright = data.copyright;
				this.error = data.msg;
				data.media_type === "video"
					? (this.isVideo = true)
					: (this.isVideo = false);
				console.log(this.dateFromField);
			})
			.catch((error) => console.error(error));
	},
	methods: {
		getPhoto() {
			fetch(
				`https://secure-citadel-62036.herokuapp.com/${this.uri}&date=${moment(
					this.dateFromField
				).format(moment.HTML5_FMT.DATE)}`
			)
				.then((res) => res.json())
				.then((data) => {
					console.log(data);
					this.title = data.title;
					this.src = data.url;
					this.explanation = data.explanation;
					this.copyright = data.copyright;
					this.error = data.msg;
					data.media_type === "video"
						? (this.isVideo = true)
						: (this.isVideo = false);
					// console.log(moment().format(moment.HTML5_FMT.DATE));
					console.log(this.dateFromField);
				})
				.catch((error) => console.error(error));
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
	margin: 40px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
	color: #42b983;
}

img {
	max-width: 75%;
}
#title {
	margin-bottom: 1rem;
}
#explanation {
	max-width: 70h;
	margin: 1rem auto;
}
</style>
