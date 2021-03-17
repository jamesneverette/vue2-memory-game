<template>
	<div class="component c-card">
		<div class="c-card__inner position-relative">
			<div class="c-card__inner-front position-absolute"></div>
			<div
				class="c-card__inner-back position-absolute"
				:style="{ backgroundColor: card.color }"
			></div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Card',

	props: {
		card: {
			required: true,
			type: Object,
		},
	},
};
</script>

<style lang="scss" scoped>
.c-card {
	cursor: pointer;
	height: 140px;
	perspective: 1000;
	width: 100%;

	&__inner {
		height: 100%;
		width: 100%;

		&-front,
		&-back {
			-webkit-backface-visibility: hidden;
			-moz-backface-visibility: hidden;
			-o-backface-visibility: hidden;
			backface-visibility: hidden;
			-webkit-transition: 0.6s;
			-webkit-transform-style: preserve-3d;
			-moz-transition: 0.6s;
			-moz-transform-style: preserve-3d;
			-o-transition: 0.6s;
			-o-transform-style: preserve-3d;
			-ms-transition: 0.6s;
			-ms-transform-style: preserve-3d;
			transition: 0.6s;
			transform-style: preserve-3d;
			top: 0;
			left: 0;
			height: 100%;
			width: 100%;
		}
		&-front {
			background-color: #4158d0;
			background-image: linear-gradient(
				43deg,
				#4158d0 0%,
				#c850c0 46%,
				#ffcc70 100%
			);
		}
		&-back {
			-webkit-transform: rotateY(-180deg);
			-moz-transform: rotateY(-180deg);
			-o-transform: rotateY(-180deg);
			-ms-transform: rotateY(-180deg);
			transform: rotateY(-180deg);
			position: absolute;
		}
	}

	&.is-toggled {
		.c-card__inner {
			&-front {
				-webkit-transform: rotateY(180deg);
				-moz-transform: rotateY(180deg);
				-o-transform: rotateY(180deg);
				-ms-transform: rotateY(180deg);
				transform: rotateY(180deg);
			}
			&-back {
				-webkit-transform: rotateY(0deg);
				-moz-transform: rotateY(0deg);
				-o-transform: rotateY(0deg);
				-ms-transform: rotateY(0deg);
				transform: rotateY(0deg);
			}
		}
	}
}
</style>
