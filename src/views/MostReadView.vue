<template>
	<div class="mt-5">
		<b-card class="mt-3" v-for="article in articles" :key="article.id">
			<b-card-title>
				<b-link :to="{ path: `/articles/${article.id}`}">{{article.title}}</b-link>
			</b-card-title>
			<b-card-sub-title>
				{{new Date(article.date).toLocaleDateString('en-GB')}}
			</b-card-sub-title>
			<b-card-text>
				{{article.content | shorten}}
			</b-card-text>

		</b-card>
	</div>
</template>

<script>
// @ is an alias to /src

export default {
	name: 'MostReadView',
	components: {
	},

	data(){
		return {
			articles: [],
			categories: []
		}
	},


	filters: {
		shorten(text){
			return text.substring(0, 20) + '...';
		}
	},

	mounted() {
		this.$axios.get('/api/articles/mostRead')
			.then(response => {
				this.articles = response.data
			})
		this.$axios.get('/api/categories')
			.then(response => {
				this.categories = response.data
			})
	}
}
</script>