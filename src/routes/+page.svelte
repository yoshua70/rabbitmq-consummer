<script lang="ts">
	import JobStatus from '$lib/jobStatus';
	import { onMount } from 'svelte';
	import JobComponent from './JobComponent.svelte';

	let messages: string[] = [];
	// let socket;

	const addMessage = (message: string) => {
		messages = [...messages, message];
	};

	onMount(() => {
		const socket = new WebSocket('ws://localhost:8080/ws');

		socket.addEventListener('open', function (event) {
			console.log('websocket connection opened.');
		});

		socket.addEventListener('message', function (event) {
			addMessage(event.data);
			console.log('received message:', event.data);
		});

		return () => {
			console.log('websocket connection closed.');
			socket.close();
		};
	});
</script>

<div class="flex flex-col my-4 gap-2">
	{#each messages as message}
		<JobComponent jobTitle={message} jobStatus={JobStatus.Completed} />
	{/each}
	<JobComponent jobTitle="Echo" jobStatus={JobStatus.Completed} />
	<JobComponent jobTitle="Clean log files" jobStatus={JobStatus.InProgress} />

	<JobComponent
		jobTitle="Download reference files"
		jobStatus={JobStatus.Failed}
		jobErrorDetails="Server returned 403"
	/>
</div>

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.gray.100);
	}
</style>
