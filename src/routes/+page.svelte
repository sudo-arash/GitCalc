<script lang="ts">
	import axios from 'axios';

	let repo = {
		owner: '',
		name: ''
	};
	let loading = false;
	let isRepoFetched = false;
	let repoData = null;
	let showModal = false;

	async function handleSubmission(event: Event) {
		event.preventDefault();

		if (!repo.owner || !repo.name) {
			alert('Please provide both the repository owner and name.');
			return;
		}

		loading = true;
		isRepoFetched = false;
		repoData = null;

		try {
			const response = await axios.get(`https://api.github.com/repos/${repo.owner}/${repo.name}`);
			repoData = response.data;
			isRepoFetched = true;
			showModal = true;
		} catch (error) {
			console.error('Error fetching repository:', error);
			alert(error.message);
		} finally {
			loading = false;
		}
	}

	function closeModal() {
		showModal = false;
	}
</script>

{#if loading}
	<div class="absolute inset-0 z-10 flex items-center justify-center bg-gray-800 bg-opacity-50">
		<div
			class="loader h-16 w-16 animate-spin rounded-full border-t-4 border-solid border-blue-500"
		></div>
	</div>
{/if}

<div class="w-full max-w-md rounded-lg bg-white p-6 shadow-lg">
	<h1 class="mb-4 text-2xl font-semibold text-gray-800">GitCalc</h1>
	<form on:submit={handleSubmission} class="space-y-4">
		<div>
			<label class="mb-1 block text-sm font-medium text-gray-700"> Repository Owner </label>
			<input
				placeholder="GitHub repo's owner"
				bind:value={repo.owner}
				required
				class="w-full rounded-lg border px-4 py-2 text-gray-800 focus:outline-none focus:ring focus:ring-blue-300"
			/>
		</div>
		<div>
			<label class="mb-1 block text-sm font-medium text-gray-700"> Repository Name </label>
			<input
				placeholder="GitHub repo's name"
				bind:value={repo.name}
				required
				class="w-full rounded-lg border px-4 py-2 text-gray-800 focus:outline-none focus:ring focus:ring-blue-300"
			/>
		</div>
		<button
			type="submit"
			class="w-full rounded-lg bg-blue-500 px-4 py-2 font-medium text-white transition hover:bg-blue-600"
			disabled={loading}
		>
			{#if loading}Loading...{:else}Fetch Info{/if}
		</button>
	</form>
</div>

{#if showModal && isRepoFetched && repoData}
	<div class="fixed inset-0 z-20 flex items-center justify-center bg-gray-800 bg-opacity-50">
		<div class="w-full max-w-3xl rounded-lg bg-white p-6 shadow-lg">
			<h2 class="mb-4 text-xl font-bold text-gray-800">Repository Information</h2>
			<div class="space-y-4">
				<div class="flex items-center space-x-2">
					<i class="fas fa-user text-blue-500"></i>
					<span class="text-gray-700"><strong>Owner:</strong> {repoData.owner.login}</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-folder text-green-500"></i>
					<span class="text-gray-700"><strong>Repo Name:</strong> {repoData.name}</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-code-branch text-purple-500"></i>
					<span class="text-gray-700"
						><strong>Default Branch:</strong> {repoData.default_branch}</span
					>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-code text-blue-500"></i>
					<span class="text-gray-700"><strong>Fork:</strong> {repoData.fork ? 'Yes' : 'No'}</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-globe text-green-500"></i>
					<span class="text-gray-700"
						><strong>URL:</strong>
						<a href={repoData.html_url} target="_blank" class="text-blue-500 underline"
							>{repoData.html_url}</a
						>
					</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-calendar-alt text-yellow-500"></i>
					<span class="text-gray-700"
						><strong>Created At:</strong> {new Date(repoData.created_at).toLocaleString()}</span
					>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-sync-alt text-purple-500"></i>
					<span class="text-gray-700"
						><strong>Updated At:</strong> {new Date(repoData.updated_at).toLocaleString()}</span
					>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-star text-yellow-500"></i>
					<span class="text-gray-700"><strong>Stars:</strong> {repoData.stargazers_count}</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-star text-yellow-500"></i>
					<span class="text-gray-700"><strong>Size:</strong> {repoData.size}kb</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-eye text-blue-500"></i>
					<span class="text-gray-700"><strong>Watchers:</strong> {repoData.watchers_count}</span>
				</div>
				<div class="flex items-center space-x-2">
					<i class="fas fa-info-circle text-red-500"></i>
					<span class="text-gray-700"><strong>Description:</strong> {repoData.description}</span>
				</div>
			</div>
			<button class="mt-4 w-full rounded-lg bg-red-500 py-2 text-white" on:click={closeModal}>
				Close
			</button>
		</div>
	</div>
{/if}
