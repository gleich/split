<script lang="ts">
	import { Card, DynamicHead } from '@gleich/ui';
	import Input from './input.svelte';

	let restaurantName: string | undefined = $state();
	let subtotal: number | undefined = $state();
	let tax: number | undefined = $state();
	let tip: number | undefined = $state();
</script>

<DynamicHead title="Bill Splitter" description="Simple bill splitter" />

<h1>Bill Splitter</h1>

<div class="sections">
	<Card>
		<h3>Initial Questions</h3>
		<div class="inputs">
			<Input
				name="Restaurant Name"
				placeholder="Daniel's Pizza"
				type="text"
				bind:value={restaurantName}
			/>
			<Input name="Subtotal" type="number" bind:value={subtotal} />
			<Input name="Tax" type="number" bind:value={tax} />
			<Input name="Tip" type="number" bind:value={tip} />
		</div>
	</Card>

	<Card>
		<h3>Output Text</h3>
		<p class="output-text">
			Alright everyone here is the breakdown for {restaurantName
				? restaurantName
				: '{restaurant name}'}!
			<br />
			<br />The general formula is this: (what u got) + (share of tax) + (share of tip) = total you
			owe me.

			<br />
			<br />
			The original bill came out to the following numbers: <br />
			Subtotal: ${subtotal ?? 0} <br />
			Tax: ${tax ?? 0} <br />
			Tip: ${tip ?? 0} <br />
			Cumulative total: ${(subtotal ?? 0) + (tax ?? 0) + (tip ?? 0)}<br />
			<br />
			Here is the breakdown:
		</p>
	</Card>
</div>

<style>
	h3 {
		margin-bottom: 15px;
	}

	.sections {
		display: flex;
		flex-direction: column;
		gap: 30px;
		margin-top: 30px;
	}

	.output-text {
		margin-top: 10px;
		font-family: 'IBM Plex Mono';
		font-size: 15px;
	}

	.inputs {
		display: flex;
	}

	.inputs {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 10px;
	}
</style>
