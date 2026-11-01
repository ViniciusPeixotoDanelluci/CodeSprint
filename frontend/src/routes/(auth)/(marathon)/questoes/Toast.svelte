<div class="toast error">
	<span> Redirecionado: A questão aberta não existe. </span>
</div>
<div class="toast warning">
	<span> Atenção: A Maratona 2026 começa em 5 minutos. </span>
</div>
<div class="toast" data-toast="sucess">
	<span> Questão enviada com sucesso! </span>
</div>

<style>
	.toast {
		--clr-toast-hue: black; /* For now, can be any color */

		height: auto;
		padding: 0.5rem 1.5rem;
		margin-bottom: 0.5rem;
		margin-inline: auto;
		text-align: center;

		color: oklch(from var(--clr-toast-hue) 8% c h);
		background: oklch(from var(--clr-toast-hue) 90% calc(c / 2) h);
		box-shadow: 0.2rem 0.15rem 0 oklch(from var(--clr-toast-hue) l c h / 0.5);
		border: 2px solid var(--clr-toast-hue);
	}

	[data-toast='sucess'] {
		--clr-toast-hue: green;
	}

	.warning {
		--clr-toast-hue: rgb(226, 178, 88);
	}

	.error {
		--clr-toast-hue: red;
	}
</style>
