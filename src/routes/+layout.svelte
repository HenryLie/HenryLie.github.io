<script>
	import '@picocss/pico';
	import './styles.css';
</script>

<header class="container">
	<nav>
		<ul>
			<li>
				<a href="/">Home</a>
			</li>
		</ul>
		<ul>
			<li><a href="/colemak2qwerty">colemak2qwerty</a></li>
		</ul>
	</nav>
</header>
<main class="container">
	<slot />
</main>

<style>
	header {
		padding-bottom: 0;
	}
</style>
