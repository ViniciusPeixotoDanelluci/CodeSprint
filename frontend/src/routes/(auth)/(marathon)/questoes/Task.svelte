<script lang="ts">
	import { resolve } from '$app/paths'
	import { ArrowRightIcon } from '@lucide/svelte'
	import type { Path } from '$app/types'

	const { index }: { index: number } = $props()
</script>

<div class="task-card flex-col pos-rel">
	<div class="task-header flex-row justify-between" aria-label="Questão e dificuldade">
		<h4>Q0{index + 1}</h4>
		<span>Dificuldade {'Fácil'}</span>
	</div>
	<div class="task-art pos-rel">
		<div class="task-background pos-abs" aria-hidden="true" style={`--bg-hue: ${190 + index * 30}`}>
			<span class="task-number pos-abs" style={`--bg-hue: ${190 + index * 30}`}>0{index + 1}</span>
		</div>
		<div class="diamonds pos-rel h-full" aria-hidden="true">
			<!-- <i class="diamondo"></i> -->
			{#each { length: 3 } as diamond}
				<i class="diamond pos-abs overflow-h" style={`--diamond-hue: ${190 + index * 35}`}></i>
			{/each}
			<!-- <i class="diamond" style={`--diamond-hue: ${190 + index * 35}`}></i>
            <i class="diamond" style={`--diamond-hue: ${190 + index * 35}`}></i>
            <i class="diamond" style={`--diamond-hue: ${190 + index * 35}`}></i> -->

			<!-- <Diamond stroke-width=3 size={diamondBaseSize*1.5} color="#17233cbf" class="diamond"/> -->
			<!-- <Diamond stroke-width=3 size={diamondBaseSize*2.3} color="#17233cbf" class="diamond"/> -->
		</div>
	</div>
	<div class="task-info__container flex-col justify-between pos-rel h-full">
		<div class="task-info flex-col pos-rel">
			<h2>Palíndromo</h2>
			<p>
				Execute um loop capaz de identificar um padrão palindrômico e retornar um valor com base
				nisso.
			</p>
		</div>
		<div class="separator w-full"></div>
		<div class="task-actions flex-row justify-between">
			<span class="score">
				Pontos: <span>200</span>
			</span>
			<a
				class="task-link flex-row align-center overflow-h"
				href={resolve(('/questoes/' + (index + 1)) as Path)}
			>
				<ArrowRightIcon class="task-link__arrow flex-rol" />
			</a>
		</div>
	</div>
</div>

<style>
	.task-header {
		font-family: 'IBM Plex Mono';
		padding: 0.65rem;
		h4 {
			margin: 0;
			align-self: center;
		}
		span {
			font-family: 'Geist Sans';
		}
	}

	.task-card {
		height: clamp(18rem, 22rem, 10vh);
		width: clamp(23rem, 30vw, 32rem);
		background: var(--clr-bg-task-card);
		border: 1px solid #d8d9d3;
		box-shadow: 4px 4px 0 #deded8;
		transition:
			transform 0.18s,
			box-shadow 0.18s;
		&:hover {
			transform: translate(-2px, -2px);
			box-shadow: 6px 6px 0 #d4d4cd;
		}
	}

	.task-art {
		min-height: clamp(6.6rem, 6.7rem, 7rem);
		z-index: 1;
	}

	.task-background {
		inset: 0;
		opacity: 0.6;
		background-image:
			linear-gradient(black 1px, transparent 1px),
			linear-gradient(90deg, black 1px, transparent 1px);
		background-size: 18px 18px;
		background-color: hsl(var(--bg-hue, 40deg) 55% 45%);
		border-block: 1px solid #d8d9d3;
	}

	.task-number {
		font-size: 6rem;
		/*color: #ffa2d5f8; /*#f7f4e8ee;*/
		color: hsl(var(--bg-hue) 85% calc(35% / 2));
		font-family: 'IBM Plex Mono';
		right: 5%;
		top: 10%;
		overflow: hidden;
		font-weight: 600;
	}

	.diamonds {
		/* --diamond-hue: calc(190 + sibling-index() * 30); #45d5e7; */
		/* --clr-d: hsl(var(--diamond-hue) 55% 25%); */

		:global(.diamond) {
			min-width: calc((sibling-index() * 22px) * 0.6);
			min-height: calc((sibling-index() * 22px) * 0.6);
			border: 3px solid hsl(var(--diamond-hue) 55% 25%); /*#022369e3;*/
			transform: rotate(45deg);
			overflow: hidden;
		}

		:global(& > :nth-child(1)) {
			min-width: calc((sibling-index() * 22px) * 0.8);
			min-height: calc((sibling-index() * 22px) * 0.8);
			top: 10%;
			right: 80%;
		}

		:global(& > :nth-child(2)) {
			border-width: 5px;
			right: 70%;
			top: 25%;
		}

		:global(& > :nth-child(3)) {
			border-width: 7px;
			right: 80%;
			top: 45%;
		}
	}

	.task-info__container {
		padding: 0.7rem;
		background: var(--clr-bg-task-card);
		z-index: 2;
	}

	.task-info {
		font-family: 'Space Grotesk';
		h2 {
			margin-block: 0 0.15rem;
			margin-inline: 0.15rem;
		}
		p {
			font-size: var(--fs-300);
			/* margin-inline: 0.15rem; */
			margin-inline: 0.55rem;
			color: gray;
		}
	}

	.separator {
		height: 1px;
		align-self: center;
		margin-block-end: clamp(0.3rem, 0.25rem, 1rem);
		border-bottom: 1px solid #d8d9d3;
	}

	.task-actions {
		margin-inline: 0.3rem;
		align-items: center;
	}

	.score {
	}

	.task-link {
		border: 2px solid black;
		transition:
			transform 0.18s,
			background-color 0.18s;
		:global(.task-link__arrow) {
			color: black;
			width: max-content;
			transition: color 0.18s;
		}
		&:hover {
			background-color: black;
			:global(.task-link__arrow) {
				color: #45d5e7;
				stroke-color: #45d5e7;

				animation: arrow-slide 1.55s cubic-bezier(0.77, 0, 0.175, 1) forwards infinite;
				transform-origin: right;
			}
		}
	}

	@keyframes arrow-slide {
		0% {
			transform: translateX(-80%);
		}
		30% {
			transform: translateX(0);
		}
		70% {
			transform: translateX(0);
		}
		/* 90% {
            transform: translateX(-50%);
        } */
		100% {
			transform: translateX(150%);
		}
	}
</style>
