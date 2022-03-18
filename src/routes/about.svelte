<div class="box">
	<h1>About</h1>
	<div class="img">
		<img src="/static/cat.svg" alt="profile" />
	</div>
	<p><a href="mailto:bigfatcat0725@gmail.com">bigfatcat0725@gmail.com</a></p>
	<p><a href="https://github.com/bigfatcat-0725">https://github.com/bigfatcat-0725</a></p>
</div>

<svelte:head>
	<meta name="description" content="about page" />
</svelte:head>

<style>
	.box {
		padding: 1rem;
		text-align: center;
	}
	h1 {
		font-size: 3rem;
		margin-bottom: 2rem;
	}
	img {
		width: 15rem;
		height: 15rem;
		background-color: #333333;
		border-radius: 50%;
		margin: 0 auto;
		object-fit: contain;
		margin-bottom: 2rem;
	}
	p {
		font-size: 1.5rem;
	}
	p:hover {
		color: gray;
	}
</style>
