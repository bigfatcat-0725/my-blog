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

<div class="box">
	<div class="tags">
		<p>Tags 📌</p>
		<ul>
			<li>
				<a href="/tags/tech"># tech</a>
			</li>
			<li>
				<a href="/tags/spiritual"># spiritual</a>
			</li>
			<li>
				<a href="/tags/personal"># personal</a>
			</li>
		</ul>
	</div>
	<div class="posts">
		<ul class="post-cards">
			{#each dateSortedPosts as { path, metadata: { title, description, tags, date } }}
				<li class="post-card">
					<!-- <a href={`/posts/${path.replace('.md', '')}`}>{title}</a>
					<p class="">{new Date(date).toDateString()}</p>
					<p>
						{#each tags as tag}
							<a class="" href={`/tags/${tag}`}>#{tag}</a>
						{/each}
					</p> -->
					<div class="card card-compact bg-base-300 shadow-xl">
						<figure>
							<img src="https://api.lorem.space/image/shoes?w=400&h=225" alt="Shoes" />
						</figure>
						<div class="card-body">
							<h2 class="card-title">{title}</h2>
							<p class="">{new Date(date).toDateString()}</p>
							<p>{description}</p>
							<div class="card-actions justify-end">
								<p>
									{#each tags as tag}
										<a class="" href={`/tags/${tag}`}>#{tag}</a>
									{/each}
								</p>
								<a href={`/posts/${path.replace('.md', '')}`} class="btn btn-primary">READ MORE</a>
							</div>
						</div>
					</div>
				</li>
			{/each}
		</ul>
	</div>
</div>

<style>
	.box {
		padding: 1rem;
		display: flex;
	}
	.tags {
		flex: 1;
	}
	.tags p {
		margin-bottom: 1rem;
	}
	.tags li {
		margin-bottom: 0.5rem;
	}
	.tags a {
		white-space: nowrap;
	}
	.posts {
		flex: 9;
		margin-left: 1rem;
	}
	.post-cards {
		display: flex;
		flex-wrap: wrap;
	}
	.post-card {
		margin-left: 1rem;
		margin-bottom: 1rem;
		width: 100%;
	}
</style>
