<script lang="ts">
	let title = '';
	let content = '';
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

	function deleteNote(noteId: number) {
		const filteredNotes = notes.filter((n) => n.id !== noteId);
		notes = filteredNotes;
	}
	function createNote() {
		const newNote: (typeof notes)[0] = {
			content,
			title,
			id,
			isEditing: false
		};
		id++;

		notes = [...notes, newNote];

		title = '';
		content = '';
	}
	function prepareNoteForEdit(note: (typeof notes)[0]) {
		note.isEditing = !note.isEditing;
		notes = notes;
	}
	function finishEdit(note: (typeof notes)[0]) {
		note.isEditing = false;
		notes = notes;
	}
</script>

<section>
	<div>
		<form
			on:submit|preventDefault={createNote}
			style="margin-bottom: 30px; display: flex; flex-direction: column; gap: 10px; width: 50%"
		>
			<p>Create note</p>
			<input type="text" bind:value={title} placeholder="Title" />
			<textarea bind:value={content} placeholder="Content" />
			<input type="submit" value="Save" />
		</form>
	</div>

	{#each notes as note}
		<div style="border: 1px solid #dedede; padding: 8px">
			{#if note.isEditing}
				<form
					on:submit|preventDefault={() => finishEdit(note)}
					style="margin-bottom: 30px; display: flex; flex-direction: column; gap: 10px; width: 50%"
				>
					<input
						type="text"
						value={note.title}
						on:change={(e) => (note.title = e.currentTarget?.value)}
					/>
					<textarea
						value={note.content}
						on:change={(e) => (note.content = e.currentTarget?.value)}
					/>

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

			<button on:click={() => prepareNoteForEdit(note)}>
				{note.isEditing ? 'Cancel' : 'Edit'}
			</button>
			<button on:click={() => deleteNote(note.id)}> Delete </button>
		</div>
	{/each}
</section>
