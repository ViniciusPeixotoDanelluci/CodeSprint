<script>
	import { ArrowLeft, ChevronDown, CircleCheck, Expand, Play, RotateCcw, Send } from "@lucide/svelte"

</script>

<header class="toolbar flex-row">
	<div class="">
		<div class="toolbar__separator"></div>
        <button>
            <RotateCcw />
        </button>
        <button>
            <Expand />
        </button>
	</div>
    <div>
        <select>
            <option value="csharp">C# </option>
            <option value="js">JavaScript</option>
            <option value="python">Python</option>
            <option value="java"> Java </option>
        </select>
        <ChevronDown
            size={16}
            color="gray"
            style="position: absolute;
                margin-left: -1.5rem;
                margin-top: 0.5rem;
                pointer-events: none;"
        />
    </div>
</header>

<style>

</style>