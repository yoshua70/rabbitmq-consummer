<script>
	import JobStatus from '$lib/jobStatus';
	import JobComponent from './JobComponent.svelte';
</script>

<div class="flex flex-col my-4 gap-2">
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
