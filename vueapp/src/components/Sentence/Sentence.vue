<template>
	<div class="sentenceCardContainer grey lighten-5">
		<v-card
			outlined
			class="px-4 sentenceCard"
		>
			<v-card-title>
				Sentence
				<v-spacer />
				<v-btn
					class="mx-1"
					color="primary"
					@click="$emit('speakSentence')"
				>
					<v-icon class="pr-2">
						record_voice_over
					</v-icon>
					Speak
				</v-btn>
				<v-btn
					class="mx-2"
					color="primary"
					@click="$emit('clearSentence')"
				>
					<v-icon class="pr-2">
						clear
					</v-icon>
					Clear
				</v-btn>
			</v-card-title>
			<v-container class="py-0">
				<p
					v-if="tilePadToDisplay.length === 0"
					class="body-2"
				>
					Add tiles to this sentence by tapping on them below.
				</p>
				<v-row
					v-else
					dense
					class="mb-4"
				>
					<v-col
						v-for="(tile, tileIndex) in tilePadToDisplay"
						:key="tileIndex"
						:cols="
							$vuetify.breakpoint.xsOnly
								? 4
								: $vuetify.breakpoint.smAndDown
									? 3
									: 1
						"
						class="d-flex child-flex"
					>
						<Tile
							:tile-data="tile"
							in-sentence-component
							:sentence-index="tileIndex"
							@removeFromSentence="$emit('removeFromSentence', $event)"
						/>
					</v-col>
				</v-row>
			</v-container>
		</v-card>
	</div>
</template>

<script>
import Tile from '@/components/TilePad/Tile';

export default {
	name: 'Sentence',
	components: {
		Tile
	},
	props: {
		tilePadToDisplay: {
			type: Array,
			default () {
				return [];
			}
		}
	}
};
</script>
<style scoped>
	.sentenceCardContainer {
		position: -webkit-sticky;
		position: sticky;
		top: 56px;
		z-index: 100;
		padding: 5px;
		background-color: white;
	}
</style>
