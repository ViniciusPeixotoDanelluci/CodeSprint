<script lang="ts">
	import CodeMirror from 'svelte-codemirror-editor'
	import { githubDark } from '@fsegurai/codemirror-theme-github-dark'
	import { csharp } from '@replit/codemirror-lang-csharp'

	let code: string = $state('')

	async function awaitStoredCode() {
		const storedCode = new Promise<string>((resolve) => {
			resolve(localStorage.getItem('code')!)
		})

		const result = await storedCode

		code = result
	}

	function updateCode(code: string) {
		console.log('Código:', code)
		localStorage.setItem('code', code)
	}
</script>

<CodeMirror
	bind:value={code}
	onchange={updateCode}
	onready={awaitStoredCode}
	lang={csharp()}
	theme={githubDark}
	class="codemirror w-full h-full"
/>

<style>
	:global(.codemirror) {
	}

	:global(.codemirror .cm-editor) {
		height: 100%;
		min-height: 0;
	}
	:global(.codemirror .cm-scroller) {
		height: 100%;
		overflow: auto;
	}
</style>
