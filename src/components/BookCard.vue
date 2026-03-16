<template>
  <div class="book-card" :class="{ completed: book.completed }">
    <div class="book-info">
      <h3>{{ book.title }}</h3>
      <p class="author">{{ book.author }}</p>
      <span class="genre">{{ book.genre }}</span>
      <span v-if="book.favorite" class="favorite-badge">⭐ Любимая</span>
    </div>

    <div class="book-actions">
      <div v-if="book.completed" class="rating">
        <span
          v-for="star in 5"
          :key="star"
          @click="$emit('rate', star)"
          :class="{ active: star <= book.rating }"
        >
          ★
        </span>
      </div>

      <button
        class="btn btn-favorite"
        :class="{ active: book.favorite }"
        @click="$emit('toggle-favorite')"
        title="Добавить в избранное"
      >
        {{ book.favorite ? '★' : '☆' }}
      </button>

      <button
        class="btn btn-secondary"
        @click="$emit('toggle')"
      >
        {{ book.completed ? 'Прочитано' : 'Отметить' }}
      </button>

      <button class="btn btn-danger" @click="$emit('delete')">✕</button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  book: { type: Object, required: true }
})
defineEmits(['toggle', 'delete', 'rate', 'toggle-favorite'])
</script>

<style scoped>
.book-card {
  background: white;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s;
}
.book-card.completed {
  background: #f0f7f0;
  opacity: 0.9;
}
.book-info {
  flex: 1;
}
.book-info h3 {
  margin-bottom: 4px;
  color: #333;
  display: flex;
  align-items: center;
  gap: 8px;
}
.author {
  color: #666;
  font-size: 0.9em;
  margin-bottom: 4px;
}
.genre {
  background: #e0e0e0;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.8em;
}
.favorite-badge {
  margin-left: 8px;
  color: gold;
  font-weight: bold;
}
.book-actions {
  display: flex;
  gap: 8px;
  align-items: center;
}
.rating {
  display: flex;
  gap: 2px;
}
.rating span {
  font-size: 20px;
  cursor: pointer;
  color: #ccc;
  transition: transform 0.2s;
}
.rating span.active {
  color: gold;
}
.rating span:hover {
  transform: scale(1.2);
}
.btn {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
  transition: background 0.3s;
}
.btn-secondary {
  background: #2196F3;
  color: white;
}
.btn-secondary:hover {
  background: #1e87db;
}
.btn-danger {
  background: #f44336;
  color: white;
  padding: 8px 12px;
}
.btn-danger:hover {
  background: #da190b;
}
.btn-favorite {
  background: transparent;
  color: gold;
  font-size: 1.4em;
  padding: 4px 8px;
}
.btn-favorite.active {
  color: gold;
}
</style>