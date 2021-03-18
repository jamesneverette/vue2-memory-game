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
	width: 100%;

	&__inner {
		height: 100%;
		width: 100%;

		&-front,
		&-back {
			backface-visibility: hidden;
			transition: 0.5s;
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
			-ms-transform: rotateY(-180deg);
			transform: rotateY(-180deg);
			position: absolute;
		}
	}

	&.is-toggled {
		.c-card__inner {
			&-front {
				transform: rotateY(180deg);
			}
			&-back {
				transform: rotateY(0deg);
			}
		}
	}
	&.is-matched {
		opacity: 0;
		pointer-events: none;
		transition: 0.5s;
	}
}
</style>
