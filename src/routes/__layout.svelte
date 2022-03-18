<script>
	import '../app.css'

	import { onMount } from 'svelte'
	import { themeChange } from 'theme-change'
	import ThemeSelect from '$lib/components/theme-select.svelte'

	onMount(async () => {
		themeChange(false)
	})
</script>

<div class="drawer h-screen w-full">
	<input id="my-drawer-3" type="checkbox" class="drawer-toggle" />
	<div class="drawer-content flex flex-col">
		<!-- Navbar -->
		<div class="w-full navbar bg-base-300 px-4">
			<div class="flex-none lg:hidden">
				<label for="my-drawer-3" class="btn btn-square btn-ghost">
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						class="inline-block w-6 h-6 stroke-current"
						><path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 6h16M4 12h16M4 18h16"
						/></svg
					>
				</label>
			</div>
			<div class="flex-1">
				<div class="btn bg-base-300">
					<img class="w-8 mr-4" src="../../static/cat.svg" alt="cat logo" />
					BIGFATCAT0725
				</div>
			</div>
			<div class="flex-none hidden lg:block">
				<ul class="menu menu-horizontal">
					<!-- Navbar menu content here -->
					<li>
						<a href="/">Home</a>
					</li>
					<li><a href="/posts">Posts</a></li>
					<li><a href="/about">About</a></li>
				</ul>
				<ThemeSelect />
			</div>
		</div>
		<!-- Page content here -->
		<slot />
	</div>
	<div class="drawer-side">
		<label for="my-drawer-3" class="drawer-overlay" />
		<ul class="menu p-4 overflow-y-auto w-80 bg-base-100">
			<!-- Sidebar content here -->
			<li><a href="/">Home</a></li>
			<li><a href="/posts">Posts</a></li>
			<li><a href="/about">About</a></li>
		</ul>
	</div>
</div>

<!-- Footer -->
<footer class="footer footer-center p-4 bg-base-300 text-base-content">
	<div>
		<p>Copyright © 2022 - All right reserved by bigfatcat0725</p>
	</div>
</footer>

<style>
	.btn {
		border-radius: 0;
		border: 0;
	}
</style>
