<template>
	<img
		id="nasaLogo"
		alt="Nasa logo"
		src="https://i.pinimg.com/originals/3e/a7/94/3ea794842922b855c722dad4d36000ef.png"
	/>
	<Apod />
</template>

<script>
import Apod from "./components/Apod.vue";

export default {
	name: "App",
	components: {
		Apod,
	},
};
</script>

<style>
body {
	background: cornflowerblue;
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #fff;
	font-weight: 600;
	margin-top: 60px;
}

#nasaLogo {
	max-width: 150px;
}
</style>
