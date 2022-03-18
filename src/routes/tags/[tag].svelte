<script context="module">
	const allPosts = import.meta.glob('../posts/*.md')

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
	// export let tag
</script>

<svelte:head>
	<meta name="description" content="tags" />
</svelte:head>

<div class="box">
	<div class="tags">
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
			{#each filteredPost as { path, metadata: { title, description, tags, date } }}
				<li class="post-card">
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
