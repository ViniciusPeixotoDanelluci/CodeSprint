<script lang="ts">
	let { data = 
		{ cases: [
			{
				id: 1,
				inputs: ["121"],
			},
			{
				id: 2,
				inputs: ["-121"],
			},
			{
				id: 3,
				inputs: ["10"],
			},
			{
				id: 4,
				inputs: ["1221"]
			}
		], 
		param: ["x"]} }: {
			data?: {
				cases: { id: number, inputs: any[] }[];
				param: string[];
			};
		} = $props();

	const { cases, param } = $derived(data)

	let selectedCaseId = $derived(cases[0]!.id);
	let selectedCase = $derived(cases.find((c) => c.id === selectedCaseId))!

</script>

<div class="case-view">
	<div class="case-container">
		<div class="buttons">
			{#each cases as c, index}
				<button onclick={() => (selectedCaseId = c.id)} class:active={selectedCaseId === c.id}>
					Caso {index}
				</button>
			{/each}
		</div>
		<div class="inputs">
			<span class="parameter">{param}=</span>
			<pre>{selectedCase.inputs[0]}</pre>
		</div>
	</div>
</div>

<style>
	.case-view {
		height: 100%;
		overflow: scroll;
		background-color: var(--bg-editor-panel);
		border-radius: 0 0 0.5rem 0.5rem;
	}
	.case-container {
		margin: 1rem;
	}
	.inputs {
		margin-top: 0.75rem;
	}

	.parameter {
		font-size: small;
		color: var(--txt-editor);
	}
	.buttons {
		display: flex;
		gap: 0.5rem;
	}
	pre {
		font-size: large;
		padding: 0.55rem;
		margin-top: 0;
		background-color: var(--bg-editor-input);
		border-radius: 0.5rem;
		color: var(--txt-editor);
	}
	button {
		height: 2rem;
		padding-inline: 1rem;
		padding-block: 0.6rem;

		font-size: var(--text-sm);
		background-color: transparent;
		color: var(--txt-editor-case-btn);
		border: 0px;
		border-radius: 0.5rem;
	}
	button:hover {
		background-color: var(--bg-editor-case-btn-hover);
	}
	button.active {
		background-color: var(--bg-editor-input);
	}
</style>
