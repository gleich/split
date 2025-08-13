<script lang="ts">
	import { Card, DynamicHead } from '@gleich/ui';
	import Input from './input.svelte';
	import Person from './person.svelte';

	interface PersonData {
		name: string;
		amount: number;
	}

	let restaurantName: string | undefined = $state();
	let subtotal: number | undefined = $state();
	let tax: number | undefined = $state();
	let tip: number | undefined = $state();
	let people: PersonData[] = $state([{ name: 'Joe West', amount: 0 }]);

	const round2 = (n: number) => Math.round((n + Number.EPSILON) * 100) / 100;
	const fmt = (n?: number) => round2(n ?? 0).toFixed(2);
	const shareOf = (part?: number, total?: number, fee?: number) =>
		(total ?? 0) ? ((part ?? 0) / (total ?? 0)) * (fee ?? 0) : 0;
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
		<h3>People</h3>
		<div class="people">
			{#each people as person, index (person)}
				<Person index={index + 1} bind:name={person.name} bind:amount={person.amount} />
			{/each}
		</div>
		<button class="add-person-button" onclick={() => people.push({ name: '', amount: 0 })}
			>Add Person</button
		>
	</Card>

	<Card>
		<h3>Output Text</h3>
		<p class="output-text">
			Alright everyone here is the breakdown for {restaurantName
				? restaurantName.trim()
				: '{restaurant name}'}!
			<br />
			<br />The general formula is this: (what u got) + (share of tax) + (share of tip) = total you
			owe me.

			<br />
			<br />
			The original bill came out to the following numbers: <br />
			Subtotal: ${fmt(subtotal)} <br />
			Tax: ${fmt(tax)} <br />
			Tip: ${fmt(tip)} <br />
			Cumulative total: ${fmt((subtotal ?? 0) + (tax ?? 0) + (tip ?? 0))} <br />
			<br />
			Here is the breakdown:<br />
			{#each people as person (person)}
				- {person.name}: ${fmt(person.amount)} + ${fmt(shareOf(person.amount, subtotal, tax))} + ${fmt(
					shareOf(person.amount, subtotal, tip)
				)} = ${fmt(
					person.amount +
						shareOf(person.amount, subtotal, tax) +
						shareOf(person.amount, subtotal, tip)
				)}
				<br />
			{/each}

			<br />
			If y'all could just send it to me on Venmo when you get a chance! My account is @mattgleich.
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

	.people {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}

	.add-person-button {
		margin-top: 20px;
		padding: 8px 5px;
		width: 100%;
	}
</style>
