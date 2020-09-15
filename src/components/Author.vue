<template>
	<div class="author">

		<g-image alt="Author image" class="author__image" src="~/assets/images/author.jpg" width="180" height="180" blur="5" />

		<h1 v-if="showTitle" class="author__site-title">
			{{ $static.metadata.siteName }}
		</h1>

		<p class="author__intro">
			Develop Smarter
		</p>

		<p class="author__links">
			<a href="//twitter.com/copypastepray" target="_blank">Twitter</a>
			<a href="//stackoverflow.com/users/988683/rncrtr" target="_blank">Stack Overflow</a>
			<a href="//dev.to/copypastepray" target="_blank">Dev.to</a>
			<a href="//github.com/copypastepray" target="_blank">GitHub</a>
			<a href="//www.quora.com/profile/Ryan-Carter-38" target="_blank">Quora</a>
		</p>

	</div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
export default {
	props: ['showTitle']
}
</script>

<style lang="scss">
.author {
	margin: 0 auto;
	max-width: 500px;
	text-align: center;
	padding: calc(var(--space) / 2) 0;

	&__image {
		border-radius: 100%;
		width: 90px;
		height: 90px;
		margin-bottom: 1em;
	}

	&__intro {
		opacity: .8;
	}

	&__site-title {
		font-size: 1.5em;
	}

	&__links {
		margin-top: -.5em;
		a {
			margin: 0 .5em;
		}
	}
}
</style>
