<script lang="ts">
	import { Card } from '@gleich/ui';

	let {
		index,
		name = $bindable(),
		amount = $bindable()
	}: { index: number; name: string; amount: number } = $props();
</script>

<Card padding="0">
	<div class="container">
		<p class="index">#{index}</p>
		<input type="text" name="Name" placeholder="Joe West" bind:value={name} />
		<input type="number" name="Amount" placeholder="$67" bind:value={amount} />
	</div>
</Card>

<style>
	.container {
		display: flex;
		gap: 10px;
	}

	.index {
		font-family: 'IBM Plex Mono';
		color: grey;
		padding: 12px 15px;
		box-shadow: inset var(--box-shadow);
		background-color: var(--section-name-background-color);
		width: fit-content;
	}

	input {
		margin: 5px;
		text-align: left;
		padding-left: 20px;
		background-color: var(--background);
		border-radius: 4px;
		font-family: 'IBM Plex Mono';
	}
</style>
