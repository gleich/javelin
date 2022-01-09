<script lang="ts">
	import { Writable, writable } from 'svelte/store';
	import { flip } from 'svelte/animate';
	import { nanoid } from 'nanoid';

	interface Task {
		name: string;
		id: string;
	}

	const addTask = () => {
		tasks.set([...$tasks, { name: newTask, id: nanoid() }]);
		newTask = '';
	};

	const removeTask = (id: string) => {
		tasks.set([...$tasks.filter((t) => t.id != id)]);
	};

	let newTask = '';
	const tasks: Writable<Task[]> = writable([]);
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
			bind:value={newTask}
		/>
		<div class="tasks">
			{#each $tasks as task (task.id)}
				<div animate:flip class="task">
					<input
						on:change={() => removeTask(task.id)}
						type="checkbox"
						name={task.id}
						value={task.name}
					/>
					<label for={task.id}>{task.name}</label>
				</div>
			{/each}
		</div>
	</div>
</main>
<footer>
	<p>&copy; {new Date().getFullYear()} Matt Gleich</p>
	<a href="https://github.com/gleich/javelin" target="_blank">gleich/javelin</a>
</footer>

<style>
	main {
		width: 100vw;
		height: 100vh;
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
		max-height: 40vh;
	}

	.task {
		display: flex;
		gap: 5px;
	}

	footer {
		position: absolute;
		bottom: 0;
		width: 99%;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 20px;
	}

	a {
		color: #418fdd;
	}
</style>
