<template>
	<div id="app">
		<section class="s-board container">
			<ul
				class="component c-cards c-cards--list d-flex justify-content-center align-items-center flex-wrap"
			>
				<li
					class="c-cards__item p-1"
					v-for="(card, index) in cards"
					:key="index"
				>
					<card :card="card" />
				</li>
			</ul>
		</section>
	</div>
</template>

<script>
import Card from '@/components/Card';
export default {
	name: 'App',

	components: {
		Card,
	},

	data: () => ({
		cards: [
			{
				name: 'Orange',
				color: 'orange',
				toggled: false,
			},
			{
				name: 'Red',
				color: 'red',
				toggled: false,
			},
			{
				name: 'Blue',
				color: 'blue',
				toggled: false,
			},
			{
				name: 'Green',
				color: 'green',
				toggled: false,
			},
			{
				name: 'Yellow',
				color: 'yellow',
				toggled: false,
			},
			{
				name: 'Purple',
				color: 'purple',
				toggled: false,
			},
			{
				name: 'Grey',
				color: 'grey',
				toggled: false,
			},
			{
				name: 'Black',
				color: 'black',
				toggled: false,
			},
			{
				name: 'Teal',
				color: 'teal',
				toggled: false,
			},
			{
				name: 'Pink',
				color: 'pink',
				toggled: false,
			},
			{
				name: 'Magenta',
				color: 'magenta',
				toggled: false,
			},
			{
				name: 'Brown',
				color: 'brown',
				toggled: false,
			},
		],
	}),
};
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

.c-cards {
	&--list {
		list-style: none;
		margin: 0;
		padding: 0;
	}
	&__item {
		flex: 0 1 20%;
	}
}
</style>
