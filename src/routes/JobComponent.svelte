<script lang="ts">
	import JobStatus from '$lib/jobStatus';

	export let jobTitle: string;
	export let jobStatus: JobStatus;
	export let jobErrorDetails = '';

	const getBackgroundColor = () => {
		switch (jobStatus) {
			case JobStatus.Pending:
				return 'bg-gray-300';
			case JobStatus.InProgress:
				return 'bg-yellow-300';
			case JobStatus.Completed:
				return 'bg-green-300';
			case JobStatus.Failed:
				return 'bg-red-300';
		}
	};
</script>

<div class={`p-8 flex flex-col gap-2 ${getBackgroundColor()}`}>
	<p>Name: {jobTitle}</p>
	<p>Status: <span class="uppercase">{jobStatus}</span></p>
	{#if jobStatus === JobStatus.Failed}
		<p>Details: {jobErrorDetails}</p>
	{/if}
</div>
