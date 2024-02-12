<script lang="ts">
	import CreateNote from './CreateNote.svelte';
	import Note from './Note.svelte';

	let id = 0;

	let notes = [
		{
			title: 'test',
			content: 'content',
			id: 1,
			isEditing: false
		},
		{
			title: 'test2',
			content: 'content2',
			id: 2,
			isEditing: false
		},
		{
			title: 'test3',
			content: 'content3',
			id: 3,
			isEditing: false
		}
	];

	function createNote(event) {
		const newNote: (typeof notes)[0] = {
			...event.detail,
			id,
			isEditing: false
		};
		id++;

		notes = [...notes, newNote];

		title = '';
		content = '';
	}

	function deleteNote(event) {
		const filteredNotes = notes.filter((n) => n.id !== event.detail.noteId);
		notes = filteredNotes;
	}

	function finishEdit(event) {
		event.detail.note.isEditing = false;
		notes = notes;
	}
	function prepareNoteForEdit(event) {
		event.detail.note.isEditing = !event.detail.note.isEditing;
		notes = notes;
	}
</script>

<section>
	<CreateNote on:createNoteDispatched={createNote} />

	{#each notes as note}
		<Note
			{note}
			on:deleteNoteDispatched={deleteNote}
			on:finishEditNoteDispatched={finishEdit}
			on:prepareNoteForEditDispatched={prepareNoteForEdit}
		/>
	{/each}
</section>
