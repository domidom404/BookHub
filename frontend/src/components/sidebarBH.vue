<script setup lang="ts">
import { BookOpen, Heart, BookMarked, Wand2, Skull, BookHeart, BookMinus } from 'lucide-vue-next';

interface Genre {
  name: string;
  icon: any;
  color: string;
}

const emit = defineEmits<{
  genreSelect: [genre: string | null];
  viewChange: [view: 'feed' | 'mybooks' | 'discover' | 'community'];
}>();

const props = defineProps<{
  selectedGenre: string | null;
}>();

const handleGenreClick = (genre: string) => {
  emit('genreSelect', genre);
  emit('viewChange', 'discover');
};

const handleShelfClick = () => {
  emit('viewChange', 'mybooks');
};

const genres: Genre[] = [
  { name: 'Ficção', icon: BookOpen, color: 'text' },
  { name: 'Fantasia', icon: Wand2, color: 'text' },
  { name: 'Terror', icon: Skull, color: 'text' },
  { name: 'Romance', icon: BookHeart, color: 'text' },
  { name: 'Não-Ficção', icon: BookMinus, color: 'text' },
];
</script>

<template>
  <aside class="sidebar">
    <div class="mb-8">
      <h3 class="section-title">Minhas Estantes</h3>
      <div class="space-y-2">
        <button 
          @click="handleShelfClick"
          class="btn"
        >
          <BookOpen class="icon text" />
          <span>Lendo Atualmente</span>
        </button>
        <button 
          @click="handleShelfClick"
          class="btn"
        >
          <BookMarked class="icon text" />
          <span>Lidos</span>
        </button>
        <button 
          @click="handleShelfClick"
          class="btn"
        >
          <Heart class="icon text" />
          <span>Favoritos</span>
        </button>
      </div>
    </div>

    <div>
      <h3 class="section-title">Gêneros</h3>
      <div class="space-y-2">
        <button
          v-for="genre in genres"
          :key="genre.name"
          @click="handleGenreClick(genre.name)"
          :class="[
            'btn',
            selectedGenre === genre.name ? 'active' : ''
          ]"
        >
          <component :is="genre.icon" :class="['icon', genre.color]" />
          <span>{{ genre.name }}</span>
        </button>
      </div>
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 20%;
  background-color: #40434E;
  padding: 1.5rem;
  margin-top: 5rem;
}

.mb-8 {
  margin-bottom: 2rem;
}

.section-title {
  color: #ffffff;
  margin-bottom: 1rem;
  font-weight: 500;
}

.space-y-2 {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #ffffff;
  background: none;
  border: none;
  width: 100%;
  padding: 0.5rem;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: all 0.2s;
  text-align: left;
  font-size: 1rem;
}

.btn:hover {
  color: #912F40;
  background-color: #eef2ff;
}

.btn.active {
  color: #912F40;
  background-color: #eef2ff;
}

.icon {
  width: 1.25rem;
  height: 1.25rem;
  flex-shrink: 0;
}

.text {
  color: #a43649;
}

.text:hover{
  color: #dc2626;
}

</style>