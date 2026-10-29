<script lang="ts">
	import type { LayoutProps } from './$types';
	import Header from './Header.svelte';
	import '../common.css';

	let { children }: LayoutProps = $props();
</script>

<div class="user-layout">
	<Header />

	<main>
		{@render children()}
	</main>
</div>

<style>
	.user-layout {
		height: 100dvh;
		display: flex;
		flex-direction: column;
	}

	main {
		flex: 1;
		display: flex;
	}
</style>
