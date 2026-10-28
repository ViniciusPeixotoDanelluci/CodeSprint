<script lang="ts">
    import { Pane, Splitpanes } from 'svelte-splitpanes';
</script>

<div>Editor</div>

<div>
    <Splitpanes pushOtherPanes={false} style="min-width: 1000px;">
        <Pane minSize={10} maxSize={80} snapSize={12.555}>
            <div class="panel">
                Questão
            </div>
        </Pane>
        <Pane>
            <div class="panel">
                <Splitpanes horizontal={true} pushOtherPanes={false}>
                    <Pane minSize={10} maxSize={80} snapSize={12.555}>
                        <div class="panel">
                            Código
                        </div>
                    </Pane>
                    <Pane minSize={10} maxSize={80} snapSize={12.555}>
                        <div class="panel">
                            Terminal
                        </div>
                    </Pane>
                </Splitpanes>
            </div>
        </Pane>
    </Splitpanes>
</div>
<style>
    .panel {
        min-width: 300px;
        min-height: 300px;
        height: 600px;
    }
</style>