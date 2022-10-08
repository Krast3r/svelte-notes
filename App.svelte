<script>
  let notes = [];

  let data = {
    title: "",
    category: "",
    content: "",
    id: null
  };

  let addNote = () => {
    const newNote = {
      id: notes.length + 1,
      title: data.title,
      category: data.category,
      content: data.content
    };

    notes = notes.concat(newNote);
    data = {
      id: null,
      title: "",
      category: "",
      content: ""
    };
    console.log(notes);
  };

  let deleteNote = id => {
    console.log(id);
    notes = notes.filter(note => note.id !== id);
  };

  let isEdit = false;
  let editNote = note => {
    isEdit = true;
    data = note;
  };

  let updateNote = () => {
    isEdit = !isEdit;
    let noteDB = {
      title: data.title,
      category: data.category,
      content: data.content,
      id: data.id
    };

    let objIndex = notes.findIndex(obj => obj.id == noteDB.id);
    console.log(`Before update: ${notes[objIndex]}`);
    notes[objIndex] = noteDB;
    data = {
      id: null,
      title: "",
      category: "",
      content: ""
    };
  };
</script>
<style>
  @import url("https://fonts.googleapis.com/css?family=Nunito&display=swap");
  * {
    font-family: "Nunito", sans-serif;
  }
</style>
<section>
  <div class="container">
    <div class="row mt-5">
      <div class="col-md-6">
        <div class="card bg-dark text-white p-2 shadow">
          <div class="card-body">
            <h5 class="card-title mb-4">Add New Note</h5>
            <form>
              <div class="form-group">
                <label for="title">Title</label>
                <input
                  bind:value={data.title}
                  type="text"
                  class="form-control"
                  id="text"
                  placeholder="Note Title" />
              </div>
              <div class="form-group">
                <label for="category">Category</label>
                <select 
                  class="form-control"
                  id="category"
                  bind:value={data.category}>
                  <option selected disaabled>Selecet a category</option>
                  <option>School</option>
                  <option>Church</option>
                  <option>Home</option>
                </select>
              </div>
              <div class="form-group">
                <label for="content">Content</label>
                <textarea
                  bind:value={data.content}
                  class="form-control"
                  id="content"
                  rows="3"
                  placeholder="Note Content" />
								</div>
                {#if isEdit === false}
                  <button type="submit" on:click|preventDefault={addNote} class="btn btn-primary">Add Note</button>
                  {:else}
                  <button type="submit" on:click|preventDefault={updateNote} class="btn btn-info">Update</button>
                {/if}
            </form>
          </div>
        </div>
      </div>
      <div class="col-md-6">
      <div class="card bg-dark text-white">
        {#each notes as note}
		        <div class="card bg-dark text-white mb-3">
      			<div class="card-body">
			        <h5 class="card-title">{note.category}</h5>
				      <p class="card-text">{note.content}</p>
				      <button on:click={editNote(note)} class="btn btn-info">Edit</button>
				      <button on:click={deleteNote(note.id)} class="btn btn-danger">Delete</button>
			      </div>
		      </div>
	    {/each}
      </div>
    </div>
  </div>
</section>