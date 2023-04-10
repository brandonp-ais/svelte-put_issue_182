<script lang="ts">
	import type { ModalPushOutput } from "@svelte-put/modal";
	import ConfirmationModal from "./ConfirmationModal.svelte";
    import { modalStore } from "$lib/modals/modal-store";

	let pushed: ModalPushOutput<ConfirmationModal>;

	async function open() {
		// should get type autocompletion for pushed here
		pushed = modalStore.push({
			component: ConfirmationModal,
			props: {
				bodyContent: 'cheese'
			}
		});
		const { confirmed, trigger } = await pushed.resolve();
		if (confirmed) {
			// do something
		}
		console.log("Modal resolves to", confirmed);
		console.log("Modal was popped by", trigger);
	}
</script>

<main>
	<h1>
		@svelte-put: Typescript Errors <a
			href="https://github.com/vnphanquang/svelte-put/issues/182">#182</a
		>
	</h1>

	<button on:click={open}> Open modal </button>
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
	}

	main > * {
		margin-bottom: 1rem;
	}
</style>
