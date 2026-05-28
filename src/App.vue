<script setup>
import { ref } from 'vue'

const mediaItems = ref([])

const title = ref('')
const type = ref('Book')
const rating = ref(5)
const status = ref('In Progress')
const notes = ref('')

function addMedia() {
  const newItem = {
    id: Date.now(),
    title: title.value,
    type: type.value,
    rating: rating.value,
    status: status.value,
    notes: notes.value
  }

  mediaItems.value.push(newItem)

  title.value = ''
  type.value = 'Book'
  rating.value = 5
  status.value = 'In Progress'
  notes.value = ''
}
</script>

<template>
  <div class="app">
    <h1>Media Tracker</h1>

    <p>Track your favorite books, shows, games, and more.</p>

    <form class="media-form" @submit.prevent="addMedia">
      <input
        v-model="title"
        type="text"
        placeholder="Title"
        required
      />

      <select v-model="type">
        <option>Book</option>
        <option>Movie</option>
        <option>TV Show</option>
        <option>Anime</option>
        <option>Game</option>
      </select>

      <select v-model="rating">
        <option :value="1">1</option>
        <option :value="2">2</option>
        <option :value="3">3</option>
        <option :value="4">4</option>
        <option :value="5">5</option>
        <option :value="6">6</option>
        <option :value="7">7</option>
        <option :value="8">8</option>
        <option :value="9">9</option>
        <option :value="10">10</option>
      </select>

      <select v-model="status">
        <option>In Progress</option>
        <option>Completed</option>
        <option>Dropped</option>
      </select>

      <textarea
        v-model="notes"
        placeholder="Notes (optional)"
      ></textarea>

      <button type="submit">Add Media</button>
    </form>
    <div class="media-list">
      <div
        class="media-card"
        v-for="item in mediaItems"
        :key="item.id"
      >
        <h2>{{ item.title }}</h2>

        <p><strong>Type:</strong> {{ item.type }}</p>
        <p><strong>Rating:</strong> {{ item.rating }}/10</p>
        <p><strong>Status:</strong> {{ item.status }}</p>

        <p v-if="item.notes">
          <strong>Notes:</strong> {{ item.notes }}
        </p>
      </div>
    </div>
  </div>
</template>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background-color: #f4f4f4;
}

.app {
  max-width: 700px;
  margin: auto;
  padding: 2rem;
}

.media-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 2rem;
}

input,
select,
textarea,
button {
  padding: 0.75rem;
  font-size: 1rem;
}

textarea {
  min-height: 100px;
}

button {
  cursor: pointer;
}

.media-list {
  margin-top: 2rem;
}

.media-card {
  background: white;
  padding: 1rem;
  margin-bottom: 1rem;
  border-radius: 8px;
}

.media-card h2 {
  color: #222;
  margin-top: 0;
}
</style>