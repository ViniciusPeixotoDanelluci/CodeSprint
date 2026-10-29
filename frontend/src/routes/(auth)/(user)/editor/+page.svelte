<script lang="ts">
    import { Pane, Splitpanes } from 'svelte-splitpanes';
	import CodeEditor from './CodeEditor.svelte';
</script>

<div class="editor-container w-full-vw">
    <Splitpanes pushOtherPanes={false} style={"border-radius: 0.25rem; overflow: hidden;"}>
        <Pane minSize={20} maxSize={80} snapSize={3.555}>
            <div class="panel">
                Questão
            </div>
        </Pane>
        <Pane>
            <div class="panel">
                <Splitpanes horizontal={true} pushOtherPanes={false}>
                    <Pane minSize={20} maxSize={80} snapSize={3.555}>
                        <div>
                            <CodeEditor />
                        </div>
                    </Pane>
                    <Pane minSize={20} maxSize={80} snapSize={3.555}>
                        <div >
                            Terminal
                        </div>
                    </Pane>
                </Splitpanes>
            </div>
        </Pane>
    </Splitpanes>
</div>

<style>
    .editor-container {
        padding: 0.55rem;
    }
    .panel {
        height: 100%;
        border-radius: 5.35rem;
    }
</style>