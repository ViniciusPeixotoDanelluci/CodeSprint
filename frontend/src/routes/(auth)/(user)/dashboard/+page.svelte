<script lang="ts">
	import { MoreHorizontalIcon } from '@lucide/svelte';
    import { Semester } from './semester-type';
    import Task from './Task.svelte';

    interface Student {
        name: string, 
        semester: Semester,   
    }

    // let students: Student[] = $props()
    let students: Student[] = [
        { name: "Lucas", semester: Semester.FIRST },
        { name: "Jones", semester: Semester.FIRST },
        { name: "Luna", semester: Semester.FIRST },
    ]
</script>

<div class="dashboard">
	<main class="tasks-section">
		<!-- <h1>Resolva o máximo de questões que puder, boa sorte!</h1> -->
		<div class="task-grid">
			{#each { length: 6 } as task, index}
				<Task {index} />
			{/each}
		</div>
	</main>

	<aside class="event-container flex-col w-full" aria-label="Informações do evento e do seu time">
		<section class="event-info-container pos-rel overflow-h" aria-labelledby="event-title">
			<div class="flex-row align-center justify-between">
				<!-- <span class="event-status"><span class="status-dot"></span> Sprint ao vivo</span> -->
			    <h2 id="event-title">Maratona 2027</h2>
				<div class="event-mark" aria-hidden="true">
					<i></i><i></i><i></i><i></i><i></i><i></i>
				</div>
			</div>

			<div class="flex-col">
				<span class="timer__label">Tempo restante</span>
				<span class="timer__text" aria-label="22 horas, 47 minutos e 16 segundos">
                    <!--Colocar horário de verdade aqui-->
                    1<span>:</span>47<span>:</span>16
				</span>
			</div>

			<div
				class="timer__bar"
				role="progressbar"
				aria-label="Progresso do evento"
				aria-valuenow="60"
				aria-valuemin="0"
				aria-valuemax="100"
			>
				<span class="h-full"></span>
			</div>
			<div class="event-progress flex-row align-center justify-between">
				<span class="solved-tasks">0 / 6 resolvidos</span>
				<span class="ranking low">22° lugar</span> 
                <!--Esse low é pra indicar o quão alto vc esta, talvez, fica pra implementar alguma hora :P-->
			</div>
		</section>

		<section class="team-container flex-col overflow-h">
			<div class="team-info" aria-labelledby="team-info">
				<div class="team-heading flex-row align-center justify-between">
					<h5>Seu time</h5>
				</div>
				<h3 id="team-title">Time 6</h3>
			</div>

			<div class="team">
                <!-- {#each students as s, index}
                    <div class="student">
                        <span class="student__avatar" aria-hidden="true">L</span>
                        <span class="student__details flex-col">
                            <span class="student__name">{s.name}</span>
                            <span class="student__semester">{s.semester}</span>
                        </span>
                    </div>
                {/each} -->
				<div class="student">
					<span class="student__avatar" aria-hidden="true">L</span>
					<span class="student__details flex-col">
						<span class="student__name">Lucas Rogério Camargo</span>
						<span class="student__semester">1° termo</span>
					</span>
				</div>
				<div class="student">
					<span class="student__avatar student__avatar--coral" aria-hidden="true">J</span>
					<span class="student__details flex-col">
						<span class="student__name">Jones</span>
						<span class="student__semester">1° termo</span>
					</span>
				</div>
				<div class="student">
					<span class="student__avatar student__avatar--cadetblue" aria-hidden="true">L</span>
					<span class="student__details flex-col">
						<span class="student__name">Luna</span>
						<span class="student__semester">1° termo</span>
					</span>
				</div>
			</div>
		</section>
	</aside>
</div>

<style>
	.dashboard {
		flex: 1;
		min-width: 0;
		display: grid;
		grid-template-columns: minmax(0, 1fr) 18rem;
		align-items: start;
		gap: 1.5rem;
		padding: 1.5rem;
	}

	.tasks-section {
		min-width: 0;
	}

	.task-grid {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		grid-template-rows: repeat(3, 1fr);
		padding: 1rem 0;
		gap: 0.75rem;
	}

	.event-container {
		gap: 1rem;
	}

	.event-info-container {
		padding: 1.25rem;
		color: #f8f8f4;
		background: #111b33;
		border: 1px solid #111b33;
		box-shadow: 4px 4px 0 #45d5e7;

		h2 {
			margin: 0 0 1rem;
			font-family: 'Space Grotesk';
			font-size: 1.4rem;
			font-weight: 500;
		}
	}

	.event-mark {
		display: grid;
		grid-template-columns: repeat(3, 0.5rem);
		gap: 0.22rem;
		transform: rotate(45deg);

		i {
			width: 0.45rem;
			height: 0.45rem;
			background: #246477;
			/* border-radius: 50%; */
		}

		i:nth-child(2),
		i:nth-child(5) {
			background: #45d5e7;
			opacity: 0.75;
		}
	}

	.timer__label {
		color: #9aa8c3;
		font-family: 'IBM Plex Mono';
        font-size: var(--fs-150);
		letter-spacing: 0.08em;
		text-transform: uppercase;
	}

	.timer__text {
		margin-top: 0.45rem;
		font-family: 'IBM Plex Mono';
		font-size: var(--fs-600);
		font-weight: bold;
		letter-spacing: 0.04em;

		span {
			color: #45d5e7;
			font-size: var(--fs-500);
		}
	}

	.timer__bar {
		height: 3px;
		margin: 0.7rem 0 0.7rem;
		background: #303b52;

		span {
			display: block;
			width: 60%;
			background: #45d5e7;
		}
	}

	.event-progress {
		font-size: 0.65rem;
		color: #9aa8c3;
	}

	.ranking {
		color: #e7f64a;
		font-weight: bold;
	}

	.team-container {
		color: #17233c;
		background: #fffef9;
		border: 1px solid #d8d9d3;
	}

	.team-info {
		padding: 0.75rem 1rem;
		border-bottom: 1px solid #d8d9d3;

		h3 {
			margin: 0.45rem 0 0;
			font-family: 'Space Grotesk';
			font-size: 1.2rem;
			font-weight: 500;
		}
	}

	.team-heading {
		color: #71809d;

		h5 {
			margin: 0;
			font-family: 'IBM Plex Mono';
			font-size: var(--fs-150);
			font-weight: normal;
			letter-spacing: 0.15em;
			text-transform: uppercase;
		}
	}

	.student {
		display: flex;
		align-items: center;
		gap: 0.55rem;
		min-height: 3.4rem;
		padding: 0.45rem 0.9rem;
		border-bottom: 1px solid #ecece7;
	}

	.student__avatar {
		display: grid;
		flex: 0 0 2rem;
		place-items: center;
		width: 2rem;
		height: 2rem;
		color: white;
		background: #385cf2;
		border-radius: 50%;
		font-size: 0.65rem;
		font-weight: bold;
	}

	.student__avatar--coral {
		background: coral;
	}

	.student__avatar--cadetblue {
		background: cadetblue;
	}

	.student__details {
		gap: 0.15rem;
	}

	.student__name {
		font-size: var(--fs-400);
		font-weight: bold;
	}

	.student__semester {
		color: #71809d;
		font-size: var(--fs-200);
	}
</style>
