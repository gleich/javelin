<script lang="ts">
	import { writable } from 'svelte/store';
	import { flip } from 'svelte/animate';

	const addTask = () => {
		tasks.set([...$tasks, newTaskName]);
		newTaskName = '';
	};

	const removeTask = (task: string) => {
		tasks.set([...$tasks].filter((t) => t != task));
	};

	let newTaskName = '';
	const tasks = writable([]);
</script>

<svelte:head>
	<title>javelin</title>
</svelte:head>

<main>
	<div class="container">
		<h1>javelin</h1>
		<input
			type="text"
			placeholder="New task"
			on:keydown={(k) => k.key === 'Enter' && addTask()}
			bind:value={newTaskName}
		/>
		<div class="tasks">
			{#each $tasks as task (task)}
				<div animate:flip class="task">
					<input on:change={() => removeTask(task)} type="checkbox" name={task} value={task} />
					<label for={task}>{task}</label>
				</div>
			{/each}
		</div>
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

	.container {
		min-width: 40vw;
	}

	.tasks {
		display: flex;
		flex-direction: column;
		padding-top: 30px;
	}

	.task {
		display: flex;
		gap: 5px;
	}
</style>
