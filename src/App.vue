<template>
	<div id="app">
		<section class="s-board container">
			<ul
				class="component c-cards c-cards--list d-flex justify-content-center align-items-center flex-wrap"
				v-if="allCards && allCards.length"
			>
				<li
					class="c-cards__item p-1"
					v-for="(card, index) in allCards"
					:key="index"
					@click="flipCard(card)"
					:class="{ 'is-toggled': card.toggled }"
				>
					<card
						:class="{ 'is-toggled': card.toggled }"
						:card="card"
					/>
				</li>
			</ul>
		</section>
	</div>
</template>

<script>
import { cloneDeep, shuffle } from 'lodash-es';
import Card from '@/components/Card';
export default {
	name: 'App',

	components: {
		Card,
	},

	data: () => ({
		allCards: [],
		cards: [
			{
				name: 'Orange',
				color: 'orange',
				toggled: false,
				matched: false,
			},
			{
				name: 'Red',
				color: 'red',
				toggled: false,
				matched: false,
			},
			{
				name: 'Blue',
				color: 'blue',
				toggled: false,
				matched: false,
			},
			{
				name: 'Green',
				color: 'green',
				toggled: false,
				matched: false,
			},
			{
				name: 'Yellow',
				color: 'yellow',
				toggled: false,
				matched: false,
			},
			{
				name: 'Purple',
				color: 'purple',
				toggled: false,
				matched: false,
			},
			{
				name: 'Grey',
				color: 'grey',
				toggled: false,
				matched: false,
			},
			{
				name: 'Black',
				color: 'black',
				toggled: false,
				matched: false,
			},
			{
				name: 'Teal',
				color: 'teal',
				toggled: false,
				matched: false,
			},
			{
				name: 'Pink',
				color: 'pink',
				toggled: false,
				matched: false,
			},
			{
				name: 'Magenta',
				color: 'magenta',
				toggled: false,
				matched: false,
			},
			{
				name: 'Brown',
				color: 'brown',
				toggled: false,
				matched: false,
			},
		],
		matches: 0,
		moves: 0,
		toggledCards: [],
	}),

	computed: {
		finished() {
			if (this.matches === 12) {
				return true;
			}

			return false;
		},
	},

	methods: {
		flipCard(card) {
			card.toggled = !card.toggled;

			if (this.toggledCards.length < 2) {
				this.toggledCards.push(card);
			}
			if (this.toggledCards.length === 2) {
				this.incrementMoves();
				this.matchCards();
			}
		},
		matchCards() {
			if (this.toggledCards[0].name === this.toggledCards[1].name) {
				setTimeout(() => {
					this.toggledCards.forEach((card) => {
						card.matched = true;
					});
					this.incrementMatches();
					this.toggledCards = [];
				}, 400);
			} else {
				setTimeout(() => {
					this.toggledCards.forEach((card) => {
						card.toggled = false;
					});
					this.toggledCards = [];
				}, 800);
			}
		},
		incrementMoves() {
			this.moves += 1;
		},
		incrementMatches() {
			this.matches += 1;
		},
		shuffleCards() {
			this.allCards = shuffle(
				this.allCards.concat(
					cloneDeep(this.cards),
					cloneDeep(this.cards),
				),
			);
		},
	},

	created() {
		this.shuffleCards();
	},
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
