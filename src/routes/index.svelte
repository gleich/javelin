<script lang="ts">
	const submit = (event) => {
		if (event.key === 'Enter') {
			console.log(`Adding ${newTaskName}`);
			newTaskName = '';
		}
	};

	let newTaskName = '';
</script>

<svelte:head>
	<title>javelin</title>
</svelte:head>

<main>
	<div class="container">
		<h1>javelin</h1>
		<input type="text" placeholder="New task" on:keydown={submit} bind:value={newTaskName} />
	</div>
</main>

<style>
	main {
		width: 100vw;
		height: 98vh;
		max-width: 100%;
		max-height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.container {
		min-width: 40vw;
	}

	h1 {
		font-size: 5rem;
	}

	input {
		background-color: transparent;
		color: var(--foreground-color);
		font-size: 1rem;
		border: none;
		border-bottom: 1px solid var(--foreground-color);
	}
</style>
