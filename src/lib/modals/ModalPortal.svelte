<!-- setup ModalPortal -->
<script lang="ts">
	import ModalPortal from "@svelte-put/modal/ModalPortal.svelte";

	import { modalStore } from "./modal-store";
</script>

<slot />

<ModalPortal store={modalStore} />
