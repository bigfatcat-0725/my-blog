<script context="module">
	const allPosts = import.meta.glob('./*.md')

	let body = []
	for (let path in allPosts) {
		body.push(
			allPosts[path]().then(({ metadata }) => {
				return { path, metadata }
			})
		)
	}

	export const load = async () => {
		const posts = await Promise.all(body)

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
</script>

<svelte:head>
	<meta name="description" content="posts" />
</svelte:head>

<div class="box">
	<div class="tags">
		<ul>
			<li>
				<a class="btn" href="/posts"># all</a>
			</li>
			<li>
				<a class="btn" href="/tags/workout"># workout</a>
			</li>
			<li>
				<a class="btn" href="/tags/eat"># eat</a>
			</li>
			<li>
				<a class="btn" href="/tags/dev"># dev</a>
			</li>
		</ul>
	</div>
	<div class="posts">
		<ul class="post-cards">
			{#each dateSortedPosts as { path, metadata: { thumbnail, title, tags, date } }}
				<li class="post-card">
					<div class="card card-compact bg-base-300">
						<figure>
							<img class="thumbnail" src={`${thumbnail}`} alt="thumbnail" />
						</figure>
						<div class="card-body gap-0.5">
							<h2 class="card-title tracking-wide">{title}</h2>
							<p class="mb-3">{new Date(date).toLocaleDateString()}</p>
							<div class="card-actions justify-end">
								<p>
									{#each tags as tag}
										<a class="uppercase" href={`/tags/${tag}`}>#{tag}</a>
									{/each}
								</p>
								<a href={`/posts/${path.replace('.md', '')}`} class="btn">READ MORE</a>
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
	.card-title {
		font-weight: normal;
	}
	.thumbnail {
		padding: 1rem 1rem;
		width: 30rem;
		height: 20rem;
	}
	.btn {
		font-weight: normal;
		border-radius: 0;
	}
	.card {
		border-radius: 0;
	}
	@media (min-width: 510px) {
		.post-card {
			margin-left: 1rem;
			margin-bottom: 1rem;
			width: 47%;
		}
	}
	@media (min-width: 1024px) {
		.post-card {
			margin-left: 1rem;
			margin-bottom: 1rem;
			width: 31%;
		}
	}
</style>
