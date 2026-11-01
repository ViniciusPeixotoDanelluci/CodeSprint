<script lang="ts">
	import { Pane, Splitpanes } from 'svelte-splitpanes'
	import CodeEditor from './components/CodeEditor.svelte'
	import Console from './components/Console.svelte'
    import Cases from './components/Cases.svelte';
    import Task from './components/Task.svelte';
	import Toolbar from './components/Toolbar.svelte'
	import SubmitReview from './components/SubmitReview.svelte'

	let isConsoleOpen = $state<boolean>(false)
</script>

{#snippet tab(title: string, tabType?: string)}
	<div class="panel-tab {tabType}">{title}</div>
    {#if tabType === "terminal"} 
        console.log()
    {/if}
    <!--
        Esse é o problema desses snippets, sempre tem alguma coisinha diferente em
        cada tab, então ou eu faço uma diferente com várias coisas parecidas ou 
        faço um overengineering pra poder fazer tabs modais pra essa única tela
    -->
{/snippet}

<div class="task-container w-full">
	<Splitpanes pushOtherPanes={false} style={'overflow: hidden;'}>
		<Pane class="panel-container" minSize={20} maxSize={80}>
			{@render tab("Questão 01", "description")}
			<div class="panel">
				<Task />
			</div>
		</Pane>
		<Pane class="panel-container">
			<div class="panel">
				<Splitpanes horizontal={true} pushOtherPanes={false}>
					<Pane class="panel-container editor-pane flex-col" minSize={20} maxSize={80} snapSize={3.555}>
                        {@render tab("Editor", "editor")}

						<div class="code-editor-container flex-col">
                            <Toolbar />
                            <div class="editor-area">
							    <CodeEditor />
                            </div>
                            <SubmitReview />
						</div>
					</Pane>
					<Pane class="panel-container" minSize={20} maxSize={80} snapSize={3.555}>
						<div class="panel-tab">
                            <button onclick={() => (isConsoleOpen = false)}>
                                Cases
                            </button>
                            <button onclick={() => (isConsoleOpen = true)}>
                                Console
                            </button>
                        </div>
						<div>
                			{#if isConsoleOpen === true}
                 				<Console />
                            {:else}
								<Cases  />
                            {/if}
						</div>
					</Pane>
				</Splitpanes>
			</div>
		</Pane>
	</Splitpanes>
</div>

<style>
	.task-container {
		/* width: 90vw;
		height: 90vh; */
		padding: 0.75rem;
		flex: 1;
		height: auto;
		min-height: 0;
	}

	:global(.panel-container) {
		background-color: rgb(26, 100, 75);
		border: 1px solid black;

        .panel-tab {
            color: contrast-color(black);
            padding: 0.75rem;
            font-family: 'IBM Plex Mono';
            font-size: var(--fs-300);
            letter-spacing: 0.07rem;
            background-color: color-mix(in srgb, rgb(43, 43, 48), #161b22);
        }
        
        .description {
            color: rgb(14, 13, 13);
            background-color: #f8f8f8;
        }
	}

	.panel {
		height: 100%;
		min-height: 0;
		background-color: aquamarine;
	}

	:global(.editor-pane) {
		min-height: 0;
	}

	.code-editor-container {
		flex: 1;
		min-height: 0;
	}

	.editor-area {
		flex: 1;
		min-height: 0;
		overflow: hidden;
	}

	:global(.editor-area .codemirror) {
		height: 100%;
	}

	:global(.senders) {
		flex-shrink: 0;
	}

</style>
