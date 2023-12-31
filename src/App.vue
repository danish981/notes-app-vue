
<script setup>
  import { ref } from 'vue';

  const showModal = ref(false);
  const newNoteTitle = ref('');
  const newNoteText = ref('');
  const notes = ref([]);

  window.addEventListener('keydown', (event) => {
    if (event.key === 'Escape') {
      showModal.value = false;
    }
  });

  const getRandomColor = () => {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }

  const addNewNote = () => {
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),  
      title : newNoteTitle.value,
      text: newNoteText.value,
      date: new Date().toLocaleDateString('en-US', {
        hour: 'numeric',
        minute: 'numeric',
        hour12: true
      }),
      backgroundColor: getRandomColor()
    });
    showModal.value = false;
    newNoteTitle.value = '';
    newNoteText.value = '';
  
  };

</script>

<template>
  <main>

    <div class="modal-dialog modal-dialog-centered modal show">
      <div v-if="showModal" class="overlay">
        <div class="modal-content w-50 mx-auto my-5">
          <div class="modal-header">
            <h5 class="modal-title">Add a New Note</h5>
            <button type="button" class="btn-close" @click="showModal = false"  aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <input type="text" class="form-control mb-2" v-model="newNoteTitle" placeholder="Note Title">
            <textarea class="form-control" cols="30" v-model="newNoteText" rows="10" placeholder="Write your note here..."></textarea>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="showModal = false" >Close</button>
            <button type="button" class="btn btn-primary" @click="addNewNote">Save Note</button>
          </div>
        </div>
      </div>
    </div>


    <div class="container mt-3">
      <header class="d-flex justify-content-between align-items-center">
        <h1>Notes</h1>
        <button class="btn btn-primary" @click="showModal = true">+</button>
      </header>
      <div class="row">

        <div class="card col-md-3 m-2 p-0" v-for="note in notes" >
          <div class="card-body" :style="{ backgroundColor : note.backgroundColor }">
            <h5 class="card-title">{{ note.title }}</h5>
            <p class="card-text">{{ note.text }}</p>
            <p class="card-footer text-muted">04/27/2023</p>
          </div>
        </div>
    
      </div>
    </div>
  </main>
</template>


<style scope>

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  align-items: center;
  justify-content: center;
  z-index: 1050;
}

.modal {
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.5);
}


.show {
  display: flex;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  border-radius: 5px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.card-title {
  font-size: 1.1rem;
  font-weight: 600;
}

.card-text {
  font-size: 0.9rem;
}

.card-footer {
  font-size: 0.8rem;
}
</style>







