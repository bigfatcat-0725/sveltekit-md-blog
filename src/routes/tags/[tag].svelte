<script context="module">
	const allPosts = import.meta.glob('../blog/*.md')

	let body = []
	for (let path in allPosts) {
		body.push(
			allPosts[path]().then(({ metadata }) => {
				return { path, metadata }
			})
		)
	}

	export const load = async ({ params }) => {
		console.log(params.tag)
		const posts = await Promise.all(body)
		const tag = params.tag

		const filteredPost = posts.filter((post) => {
			return post.metadata.tags.includes(tag)
		})

		return {
			params,
			props: {
				filteredPost,
				tag
			}
		}
	}
</script>

<script>
	export let filteredPost
	export let tag
</script>

<svelte:head>
	<meta name="description" content="blog tags" />
</svelte:head>

<h1>{tag}</h1>

{#each filteredPost as { path, metadata: { title } }}
	<li>
		<a href="{`/blog/${path.replace('.md', '')}`}">{title}</a>
	</li>
{/each}
