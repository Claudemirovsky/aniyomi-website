<script>
import { marked } from "marked";

export default {
	data() {
		return {
			whatsNew: "Failed to load data from GitHub.",
		};
	},

	async mounted() {
		try {
			const { data } = await this.$store.dispatch("getStableReleaseData");
			this.$data.whatsNew = marked(data.body).replace(
				/(?<=\(|(, ))@(.*?)(?=\)|(, ))/g,
				"<a href='https://github.com/$2' target='_blank' rel='noopener'>@$2</a>"
			);
		} catch (e) {
			console.error(e);
		}
	},
};
</script>

<template>
	<div class="guide whatsNew">
		<p class="title">
			<MaterialIcon icon="new_releases" />
			What's new
		</p>
		<!-- eslint-disable-next-line vue/no-v-html -->
		<div v-html="whatsNew"></div>
		<div class="note">
			<p>
				View the full release
				<a href="https://github.com/aniyomiorg/aniyomi/releases/latest" target="_blank" rel="noopener">here</a>
			</p>
		</div>
	</div>
</template>

<style lang="stylus">
.whatsNew
	.title
		text-align center
	div
		white-space
		h3
			font-size 1.1rem
</style>
