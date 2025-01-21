<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<div class="relative flex min-h-screen items-center justify-center bg-gray-100 p-4">
	{@render children()}
</div>

<div class="absolute bottom-4 left-1/2 flex -translate-x-1/2 transform space-x-4">
	<a
		href="https://github.com/sudo-arash/gitcalc"
		target="_blank"
		class="flex items-center space-x-2 rounded-lg bg-gray-800 px-4 py-2 text-white transition hover:bg-gray-700"
	>
		<i class="fab fa-github text-lg"></i>
		<span class="text-sm">Star on GitHub</span>
	</a>

	<a
		href="https://github.com/sudo-arash/gitcalc/fork"
		target="_blank"
		class="flex items-center space-x-2 rounded-lg bg-gray-800 px-4 py-2 text-white transition hover:bg-gray-700"
	>
		<i class="fab fa-github text-lg"></i>
		<span class="text-sm">Fork on GitHub</span>
	</a>

	<a
		href="https://github.com/sudo-arash/gitcalc/issues"
		target="_blank"
		class="flex items-center space-x-2 rounded-lg bg-gray-800 px-4 py-2 text-white transition hover:bg-gray-700"
	>
		<i class="fas fa-exclamation-circle text-lg"></i>
		<span class="text-sm">Report Issues</span>
	</a>
</div>
