<template>
	<div id="app">
		<MainHeader :moves="moves" :matches="matches" :finished="finished" />
		<section class="s-board container">
			<ul
				class="component c-cards c-cards--list d-flex justify-content-center align-items-center flex-wrap"
				v-if="deck && deck.length"
			>
				<li
					class="c-cards__item p-1"
					v-for="(card, index) in deck"
					:key="index"
					@click="
						!card.matched &&
						toggledCards.length < 2 &&
						!card.toggled
							? flipCard(card)
							: undefined
					"
					@keyup.enter="
						!card.matched &&
						toggledCards.length < 2 &&
						!card.toggled
							? flipCard(card)
							: undefined
					"
					tabindex="1"
				>
					<card
						:class="[
							{ 'is-toggled': card.toggled },
							{ 'is-matched': card.matched },
						]"
						:card="card"
					/>
				</li>
			</ul>
		</section>
		<button
			class="component c-button position-fixed py-2 px-4"
			@click="reset(deck)"
		>
			Reset
		</button>
	</div>
</template>

<script>
import { card } from '@/classes';
import { cloneDeep, shuffle } from 'lodash-es';
import Card from '@/components/Card';
import MainHeader from '@/components/MainHeader';
export default {
	name: 'App',

	components: {
		Card,
		MainHeader,
	},

	data: () => ({
		colors: [
			'orange',
			'red',
			'blue',
			'green',
			'yellow',
			'purple',
			'grey',
			'black',
			'teal',
			'pink',
			'magenta',
			'brown',
		],
		deck: [],
		matches: 0,
		moves: 0,
		toggledCards: [],
	}),

	computed: {
		finished() {
			if (this.matches === this.deck.length / 2) {
				return true;
			}

			return false;
		},
	},

	methods: {
		createDeck() {
			let cards = this.colors.map((color) => {
				return new card(color);
			});

			let deck = [].concat(cards, cloneDeep(cards));

			this.shuffleDeck(deck);
		},
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
			if (this.toggledCards[0].color === this.toggledCards[1].color) {
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
		reset() {
			this.moves = 0;
			this.matches = 0;
			this.createDeck();
		},
		shuffleDeck(deck) {
			this.deck = shuffle(deck);
		},
	},

	created() {
		this.createDeck();
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
		flex: 0 1 25%;
		outline-width: 0px;

		&:focus {
			outline-width: 2px;
		}
	}
}

.c-button {
	background: #000;
	border: none;
	bottom: 12px;
	color: #fff;
	cursor: pointer;
	display: inline-block;
	line-height: 1;
	text-align: center;
	right: 12px;
	z-index: 10;
}

@media screen and (min-width: 650px) {
	.c-cards__item {
		flex: 0 1 16%;
	}
}
</style>
