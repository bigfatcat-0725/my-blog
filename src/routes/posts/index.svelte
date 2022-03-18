<script context="module">
	const allPosts = import.meta.glob('./*.md')
	console.log(allPosts)

	let body = []
	for (let path in allPosts) {
		body.push(
			allPosts[path]().then(({ metadata }) => {
				console.log({ path, metadata })
				return { path, metadata }
			})
		)
	}

	export const load = async () => {
		const posts = await Promise.all(body)
		console.log(posts)

		return {
			props: {
				posts
			}
		}
	}
</script>

<script>
	// @ts-nocheck

	export let posts

	const dateSortedPosts = posts.sort((post1, post2) => {
		return new Date(post2.metadata.date) - new Date(post1.metadata.date)
	})

	console.log(dateSortedPosts)
</script>

<svelte:head>
	<meta name="description" content="posts" />
</svelte:head>

<h1>Posts</h1>
<ul>
	{#each dateSortedPosts as { path, metadata: { title, tags, date } }}
		<li>
			<a href={`/posts/${path.replace('.md', '')}`}>{title}</a>
			<p class="">{new Date(date).toDateString()}</p>
			<p>
				{#each tags as tag}
					<a class="" href={`/tags/${tag}`}>#{tag}</a>
				{/each}
			</p>
		</li>
	{/each}
</ul>
