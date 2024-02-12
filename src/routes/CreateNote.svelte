<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let title = '';
	let content = '';

	function createNoteDispatched() {
		dispatch('createNoteDispatched', { title, content });
		title = '';
		content = '';
	}
</script>

<form
	on:submit|preventDefault={createNoteDispatched}
	style="margin-bottom: 30px; display: flex; flex-direction: column; gap: 10px; width: 50%"
>
	<p>Create note</p>
	<input type="text" bind:value={title} placeholder="Title" />
	<textarea bind:value={content} placeholder="Content" />
	<input type="submit" value="Save" />
</form>
