<script lang="ts">
	let {
		name,
		placeholder,
		type,
		value = $bindable()
	}: {
		name: string;
		placeholder?: string | undefined;
		type: string;
		value: string | number | unknown;
	} = $props();

	const currency = type === 'number';
</script>

<div class="container">
	<input
		class={currency ? 'currency' : ''}
		{name}
		{type}
		placeholder={currency ? '0' : placeholder}
		bind:value
	/>
	<p>{name}</p>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100%;
	}

	input {
		border: 1px solid var(--border);
		padding: 10px;
		text-align: center;
		background-color: var(--background);
		font-family: 'IBM Plex Mono';
		margin: 5px;
		outline: none;
		border-radius: 3px;
		font-size: 16px;
		width: 100%;
	}

	.currency {
		position: relative;
	}

	.currency::before {
		content: '$';
		position: absolute;
		left: 10px;
	}

	input[type='number'] {
		appearance: textfield;
		-moz-appearance: textfield;
	}
	input[type='number']::-webkit-inner-spin-button,
	input[type='number']::-webkit-outer-spin-button {
		-webkit-appearance: none;
		margin: 0;
	}

	input:focus {
		border: 1px solid var(--blue-foreground);
	}

	.container p {
		text-align: center;
		font-size: 14px;
	}
</style>
