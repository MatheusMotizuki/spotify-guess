<script>
	export let showModal; // boolean

	let dialog; // HTMLDialogElement

	$: if (dialog && showModal) dialog.showModal();
</script>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-noninteractive-element-interactions -->
<dialog
	bind:this={dialog}
	on:close={() => (showModal = false)}
	on:click|self={() => dialog.close()}
>
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div on:click|stopPropagation>
		<slot name="header" />
		<hr />
		<slot />
		<hr />
		<!-- svelte-ignore a11y-autofocus -->
        <div class="close-container">
            <button autofocus on:click={() => dialog.close()}>close modal</button>
        </div>
	</div>
</dialog>

<style>
	dialog {
		width: 45vw;
		padding: 0;
		border: none;
		border-radius: 30px;
        background-color: #191414;
	}
	dialog::backdrop {
		background: rgba(0, 0, 0, 0.7); /* Darker background color */
	}
	dialog > div {
		padding: 2em; /* More padding for the content inside the modal */
	}
	dialog[open] {
		animation: zoom 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
	}
	@keyframes zoom {
		from {
			transform: scale(0.95);
		}
		to {
			transform: scale(1);
		}
	}
	dialog[open]::backdrop {
		animation: fade 0.2s ease-out;
	}
	@keyframes fade {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	.close-container {
		display: flex;
        justify-content: center;
	}
</style>
