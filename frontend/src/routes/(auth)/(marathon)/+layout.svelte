<script lang="ts">
	import Header from './Header.svelte'
	import type { LayoutProps } from './$types'

	import '../common.css'

	let { children }: LayoutProps = $props()
</script>

<div class="h-full-vh flex-col">
	<Header />
	{@render children()}
</div>
