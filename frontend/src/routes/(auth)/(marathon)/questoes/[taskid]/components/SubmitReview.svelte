<script>
	import { Play, Send } from "@lucide/svelte"


</script>
<div class="senders flex-row">
    <button class="editor-play-btn"><Play size={16} /><em>Run</em></button>
    <button class="editor-send-btn"><Send size={16} />Enviar</button>
</div>

<style>
    .senders {
        /* height: 100%; */
        min-height: 2rem;
    }
</style>