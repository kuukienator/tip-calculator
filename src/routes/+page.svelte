<script lang="ts">
	let amountPaid = 0;
	let percentageOption = 1;
	let customPercentage = 15;

	const percentageOptions = [
		{
			id: 1,
			value: 0.05,
			label: '5%'
		},
		{
			id: 2,
			value: 0.1,
			label: '10%'
		}
	];

	const round = (total: number): string => total.toFixed(2);

	const calculateWithTip = (paid: number, tipPercentage: number): string => {
		return round(paid + paid * tipPercentage);
	};

	const onClearClick = () => {
		amountPaid = 0;
	};

	$: tipPercentage =
		percentageOption === 3
			? customPercentage / 100
			: percentageOptions.find((e) => e.id === percentageOption)?.value || 0.1;
	$: withTip = calculateWithTip(amountPaid, tipPercentage);
	$: console.log('amountPaid', amountPaid, withTip);
	$: console.log('tipPercentage', tipPercentage);
</script>

<svelte:head>
	<title>Tip Calculator</title>
	<meta name="description" content="Tip Calculator - How much should you tip?" />
</svelte:head>

<section class="container">
	<p class="text">Amount to pay:</p>
	<p class="amountInputWrapper">
		<input
			type="number"
			bind:value={amountPaid}
			class="amountInput bigText"
			min="0"
			aria-label="Amount to pay"
		/>
		<span class="amountInputReset">
			<button on:click={onClearClick} aria-label="Clear amount to pay">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="24"
					height="24"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
					class="feather feather-x"
					><line x1="18" y1="6" x2="6" y2="18" /><line x1="6" y1="6" x2="18" y2="18" /></svg
				></button
			>
		</span>
	</p>

	<p class="text">Tip percentange:</p>
	<div class="percentageInputWrapper">
		{#each percentageOptions as { id, label }}
			<div>
				<input
					type="radio"
					bind:group={percentageOption}
					name="percentage"
					value={id}
					id={`percentage-${id}`}
				/>
				<label for={`percentage-${id}`} class="radioButtonLabel">{label}</label>
			</div>
		{/each}
		<div>
			<input
				type="radio"
				bind:group={percentageOption}
				name="percentage"
				value={3}
				id="percentage-3"
			/>
			<label for="percentage-3" class="radioButtonLabelNested"
				><input
					type="number"
					bind:value={customPercentage}
					on:click={() => (percentageOption = 3)}
					class="inlineInput"
					min="0"
				/><span>%</span></label
			>
		</div>
	</div>

	<p class="text">Your total:</p>

	<p class="biggerText"><b>{withTip}</b></p>
</section>

<style>
	p {
		margin: 0;
	}

	input[type='number'] {
		-webkit-appearance: none;
		outline: none;
		background-color: #c9130b;
		border-radius: 0.5rem;
		padding: 0.2rem 0.4rem;
		color: #fefefe;
	}

	.amountInputReset button {
		border-radius: 50%;
		border: none;
		width: 2rem;
		height: 2rem;
		font-weight: bold;
		background: #010001;
		color: #fefefe;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.amountInputReset {
		position: absolute;
		top: 0;
		bottom: 0;
		right: 0.5rem;
		width: 2rem;
		display: flex;
		align-items: center;
	}

	.amountInputWrapper {
		position: relative;
	}

	.amountInput {
		border: 0.2rem solid #910f08;
		padding-right: 2.5rem !important;
	}

	input[type='radio'] {
		-webkit-appearance: none;
		appearance: none;
		background-color: #fefefe;
		margin: 0;
	}
	input[type='radio']:checked + label {
		border-radius: 0.5rem;
		background: #010001;
		cursor: default;
	}
	.radioButtonLabel {
		padding: 0.7rem;
		width: 2.5rem;
		border-radius: 0.5rem;
		background: #910f08;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.radioButtonLabel:hover {
		background: #610a05;
		cursor: pointer;
	}
	.radioButtonLabelNested {
		padding: 0.6rem;
		width: 5rem;
		border-radius: 0.5rem;
		background: #910f08;
	}
	.radioButtonLabelNested:hover {
		background: #610a05;
		cursor: pointer;
	}
	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 1.25rem;
	}

	.text {
		font-size: 1.5rem;
	}

	.bigText {
		font-size: 2rem;
	}

	.biggerText {
		font-size: 5rem;
	}

	.amountInput {
		width: 8rem;
	}

	.percentageInputWrapper {
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 1.25rem;
		gap: 0.4rem;
	}
	.percentageInputWrapper > div {
		margin: 0.2 0.2rem;
		display: flex;
	}

	.inlineInput {
		display: inline-block;
		width: 2.5rem;
		font-size: 1.25rem;
		border: none;
	}
	.inlineInput + span {
		margin-left: 0.25rem;
	}
</style>
