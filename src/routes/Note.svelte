<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let note;

	function deleteNoteDispatched(noteId: number) {
		dispatch('deleteNoteDispatched', {
			noteId
		});
	}
	function finishEditNoteDispatched() {
		dispatch('finishEditNoteDispatched', { note });
	}

	function prepareNoteForEditDispatched() {
		dispatch('prepareNoteForEditDispatched', { note });
	}
</script>

<div style="border: 1px solid #dedede; padding: 8px">
	{#if note.isEditing}
		<form
			on:submit|preventDefault={finishEditNoteDispatched}
			style="margin-bottom: 30px; display: flex; flex-direction: column; gap: 10px; width: 50%"
		>
			<input
				type="text"
				value={note.title}
				on:change={(e) => (note.title = e.currentTarget?.value)}
			/>
			<textarea value={note.content} on:change={(e) => (note.content = e.currentTarget?.value)} />

			<input type="submit" value="Update" />
		</form>
	{:else}
		<div>
			<h5>
				{note.title}
			</h5>
			<p>
				{note.content}
			</p>
		</div>
	{/if}

	<button on:click={prepareNoteForEditDispatched}>
		{note.isEditing ? 'Cancel' : 'Edit'}
	</button>
	<button on:click={() => deleteNoteDispatched(note.id)}> Delete </button>
</div>
