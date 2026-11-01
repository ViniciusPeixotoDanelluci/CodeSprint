<script lang="ts">
	import { SquareCheck, SquareX } from '@lucide/svelte'

	let { result = null, isLoading = false, casesData = [] } = $props()

	let expectedOutputs = [true, false, false]

	let testResults = $derived(result?.results || [])
	let passedCount = $derived(
		testResults.filter(
			(item: { output: any }) => item?.output === expectedOutputs[testResults.indexOf(item)]
		).length
	)

	let selectedId = $state(0)
	let selectedCase = $derived(testResults[selectedId] ?? testResults[0])
	let selectedExpected = $derived(expectedOutputs[selectedId] ?? expectedOutputs[0])
	let isTestPassed = $derived(selectedCase?.output === selectedExpected)
</script>

<div class="console-view flex-col h-full w-full">
	{#if isLoading}
		<p class="console-empty">Rodando o código...</p>
	{:else if result?.error}
		<div class="console-error">{result.error}</div>
	{:else if testResults.length === 0}
		<p class="console-empty">Rode o seu código para ver o resultado.</p>
	{:else}
		<div class="">
			<div class="console-header flex-row">
				<div class="console-summary">
					<span class={passedCount < testResults.length ? 'failed' : 'passed'}>
						{passedCount}/{testResults.length} testes passaram
					</span>
				</div>
				<div class="case-buttons">
					{#each testResults as _, index}
						<button
							onclick={() => (selectedId = index)}
							class={testResults[index].output === expectedOutputs[index] ? 'pass' : 'fail'}
						>
							Caso {index + 1}
						</button>
					{/each}
				</div>
			</div>
		</div>
		<div class="console-results flex-row w-full h-full">
			<div
				class="console-card
				{testResults[selectedId].output === selectedExpected ? 'pass' : 'fail'}
			"
			>
				<div class="console-card__head">
					<span class="test-label">
						{#if isTestPassed}
							<SquareCheck color="limegreen" /> Passou
						{/if}
						{#if !isTestPassed}
							<SquareX color="red" /> Falhou
						{/if}
					</span>
				</div>
				{#if result.results[0].stdout}
					<div class="console-card__stdout">
						<p><strong>Stdout:</strong></p>
						<pre>{selectedCase.stdout}</pre>
					</div>
				{/if}
				<div class="console-card__stdout">
					<p><strong>Esperado:</strong></p>
					<pre>{selectedExpected}</pre>
				</div>
				<div class="console-card__stdout">
					<p><strong>Output:</strong></p>
					<pre>{selectedCase.output}</pre>
				</div>
			</div>
		</div>
	{/if}
</div>

<!--
<div class="console-view flex-col h-full w-full">
	{#if isLoading}
		<p class="console-empty">Running code...</p>
	{:else if result?.error}
		<div class="console-error">{result.error}</div>
	{:else if testResults.length === 0}
		<p class="console-empty">Run your code to see test results.</p>
	{:else}-->

<style>
	.console-view {
		height: 100%;
		min-height: 0;
		border-radius: 0 0 0.5rem 0.5rem;
		background-color: var(--bg-editor-panel);
		color: var(--txt-editor);
		padding: 0.9rem;
		overflow-y: auto;
		gap: 0.75rem;
		box-sizing: border-box;
	}
	.console-summary {
		height: 2rem;
		padding-inline: 0.8rem;
		padding-block: 0.2rem;
	}
	.console-header {
		gap: 0.8rem;
	}
	.console-results {
		gap: 0.6rem;
	}

	.console-card {
		width: 100%;
		min-width: 350px;
		border-radius: 0.6rem;
		padding: 0.65rem 0.8rem;
		border: 1px solid transparent;
	}

	.console-card.pass {
		border-color: var(--border-editor-pass);
		background: var(--bg-editor-pass);
	}

	.console-card.fail {
		border-color: var(--border-editor-fail);
		background: var(--bg-editor-fail);
	}

	.console-card__head {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 0.5rem;
	}

	.console-card__stdout p {
		margin: 0 0 0.25rem;
		font-size: 0.78rem;
		color: var(--txt-editor-console-muted);
	}

	.console-card__stdout pre {
		margin: 0;
		padding: 0.5rem;
		border-radius: 0.45rem;
		background: var(--bg-editor-console-pre);
		color: var(--txt-editor-console-pre);
		overflow-x: auto;
		white-space: pre-wrap;
		word-break: break-word;
	}

	.case-buttons {
		display: flex;
		gap: 0.5rem;
		overflow-x: auto;
	}

	.case-buttons button {
		height: 2rem;
		padding-inline: 0.8rem;
		padding-block: 0.4rem;

		border-radius: 0.4rem;
		background-color: var(--bg-editor-console-btn);
		color: var(--txt-editor);
		cursor: pointer;
		flex-shrink: 0;

		font-size: var(--text-sm);
	}
	.case-buttons button.pass {
		border: 1px solid var(--border-editor-pass);
		background-color: var(--bg-editor-pass-btn);
	}

	.case-buttons button.fail {
		border: 1px solid var(--border-editor-fail);
		background-color: var(--bg-editor-fail-btn);
	}

	.case-buttons button:hover {
		background-color: hsl(from currentColor h s l / 20%);
	}
</style>
