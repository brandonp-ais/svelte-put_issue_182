<script lang="ts">
	import {
		type ExtendedModalProps,
		type ExtendedModalEvents,
		createModalEventDispatcher,
	} from "@svelte-put/modal";
	import Modal from "@svelte-put/modal/Modal.svelte";

	// extending the base props
	type $$Props = ExtendedModalProps<{ bodyContent?: string }>;
	// extending the `resolve` event
	type $$Events = ExtendedModalEvents<{ confirmed: boolean }>;

	export let bodyContent = "";

	// create a custom event dispatcher with built-in helper
	const dispatch = createModalEventDispatcher<$$Events>();

	function resolve(confirmed: boolean) {
		// should get type autocompletion for dispatch here
		dispatch("resolve", {
			trigger: "custom",
			confirmed,
		});
	}
	function confirm() {
		resolve(true);
	}
	function cancel() {
		resolve(false);
	}
</script>

<!-- props is forwarded to the base Modal component -->
<!-- and the custom dispatch is also passed down -->
<Modal
	classes={{ container: "confirmation-modal bg-bg p-10" }}
	{...$$restProps}
	{dispatch}
>
	<div class="modal-content">
		<p>Confirmation Modal</p>
		<p>{bodyContent}</p>
		<div>
			<button type="button" on:click={confirm} class="c-btn-primary"
				>Confirm</button
			>
			<button
				type="button"
				on:click={cancel}
				class="c-btn-primary-outline">Cancel</button
			>
		</div>
	</div>
</Modal>
