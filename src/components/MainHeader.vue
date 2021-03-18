<template>
	<header
		class="component c-header d-flex align-items-center justify-content-between position-fixed px-2"
	>
		<div class="c-header__moves">Moves: {{ moves }}</div>
		<div class="c-header__winner" v-if="finished">WINNER!</div>
		<div class="c-header__matches">Matches: {{ matches }}</div>
	</header>
</template>

<script>
export default {
	name: 'MainHeader',

	props: {
		finished: {
			required: true,
			type: Boolean,
			default: false,
		},
		matches: {
			required: true,
			type: Number,
			default: 0,
		},
		moves: {
			required: true,
			type: Number,
			default: 0,
		},
	},
};
</script>

<style lang="scss" scoped>
@keyframes pulsate {
	0% {
		transform: scale(0.9);
	}
	50% {
		transform: scale(1.1);
	}
	100% {
		transform: scale(0.9);
	}
}

.c-header {
	background: black;
	color: white;
	font-weight: 700;
	height: 60px;
	top: 0;
	left: 0;
	width: 100%;
	z-index: 10;

	&__winner {
		animation: pulsate 2s infinite;
		transform: scale(1);
	}
}
</style>
