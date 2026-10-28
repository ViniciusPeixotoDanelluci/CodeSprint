<script lang="ts">
	import type { LayoutProps } from '../../../$types';

	let { children }: LayoutProps = $props();
</script>

<div>
	<main>
		{@render children()}
	</main>
	<header>
		<ul>
			<li>
				<a href="">Alunos</a>
			</li>
			<li>
				<a href="">Eventos</a>
			</li>
			<li>
				<a href="">Questões</a>
			</li>
			<li>
				<a href="">Times</a>
			</li>
		</ul>
	</header>
</div>
