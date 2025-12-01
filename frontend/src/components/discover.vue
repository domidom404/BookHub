<script setup lang="ts">
import { ref, computed } from 'vue';
import { Star, Plus, TrendingUp, Award, Users } from 'lucide-vue-next';

interface Book {
  id: string;
  title: string;
  author: string;
  cover: string;
  rating: number;
  reviews: number;
  genre: string;
}

const props = defineProps<{
  selectedGenre?: string | null;
}>();

const activeCategory = ref<'trending' | 'top-rated' | 'popular'>('trending');

const mockBooks: Book[] = [
  {
    id: '1',
    title: 'O Nome do Vento',
    author: 'Patrick Rothfuss',
    cover: 'https://images.unsplash.com/photo-1711185892188-13f35959d3ca?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    rating: 4.8,
    reviews: 1253,
    genre: 'Fantasia',
  },
  {
    id: '2',
    title: '1984',
    author: 'George Orwell',
    cover: 'https://images.unsplash.com/photo-1534289855405-ab820a118fc1?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    rating: 4.7,
    reviews: 2841,
    genre: 'Ficção',
  },
  {
    id: '3',
    title: 'Sapiens',
    author: 'Yuval Noah Harari',
    cover: 'https://images.unsplash.com/photo-1568667256531-7d5ac92eaa7a?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    rating: 4.9,
    reviews: 3102,
    genre: 'Não-Ficção',
  },
  {
    id: '4',
    title: 'O Hobbit',
    author: 'J.R.R. Tolkien',
    cover: 'https://images.unsplash.com/photo-1506880018603-83d5b814b5a6?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    rating: 4.6,
    reviews: 2456,
    genre: 'Fantasia',
  },
  {
    id: '5',
    title: 'A Guerra dos Tronos',
    author: 'George R.R. Martin',
    cover: 'https://images.unsplash.com/photo-1711185892188-13f35959d3ca?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    rating: 4.7,
    reviews: 1987,
    genre: 'Fantasia',
  },
  {
    id: '6',
    title: 'Drácula',
    author: 'Bram Stoker',
    cover: 'https://images.unsplash.com/photo-1534289855405-ab820a118fc1?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    rating: 4.3,
    reviews: 1654,
    genre: 'Terror',
  },
];

const filteredBooks = computed(() => {
  return props.selectedGenre
    ? mockBooks.filter(book => book.genre === props.selectedGenre)
    : mockBooks;
});
</script>

<template>
  <div class="discover-container">
    <div class="discover-content">
      <h1 class="page-title">Explorar Livros</h1>

      <div class="category-buttons">
        <button
          @click="activeCategory = 'trending'"
          :class="['category-btn', { active: activeCategory === 'trending' }]"
        >
          <TrendingUp class="icon" />
          <span>Em Alta</span>
        </button>

        <button
          @click="activeCategory = 'top-rated'"
          :class="['category-btn', { active: activeCategory === 'top-rated' }]"
        >
          <Award class="icon" />
          <span>Melhor Avaliados</span>
        </button>

        <button
          @click="activeCategory = 'popular'"
          :class="['category-btn', { active: activeCategory === 'popular' }]"
        >
          <Users class="icon" />
          <span>Mais Populares</span>
        </button>
      </div>

      <div v-if="selectedGenre" class="genre-filter">
        <h2 class="genre-title">Gênero: {{ selectedGenre }}</h2>
      </div>

      <div class="books-grid">
        <div v-for="book in filteredBooks" :key="book.id" class="book-card">
          <div class="book-cover-container">
            <img
              :src="book.cover"
              :alt="book.title"
              class="book-cover"
            />
            <div class="overlay">
              <button class="add-button">
                <Plus class="icon" />
                Adicionar à Lista
              </button>
            </div>
          </div>
          
          <div class="book-info">
            <div class="book-header">
              <div class="book-text">
                <h3 class="book-title">{{ book.title }}</h3>
                <p class="book-author">{{ book.author }}</p>
              </div>
            </div>

            <div class="rating-container">
              <div class="rating">
                <Star class="star-icon" />
                <span class="rating-value">{{ book.rating }}</span>
              </div>
              <span class="reviews">({{ book.reviews }} avaliações)</span>
            </div>

            <div class="genre-badge-container">
              <span class="genre-badge">
                {{ book.genre }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.discover-container {
  width: 80%;
  background-color: #25272D;
  padding: 1rem;
  display: flex;
  margin-left: auto;
}

.discover-content {
  max-width: 100%;
  margin: 0 auto;
}

.page-title {
  color: #FFFFFF;
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
}

.category-buttons {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.category-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  border: none;
  cursor: pointer;
  transition: all 0.2s;
  background-color: #3a3d45;
  color: #FFFFFF;
}

.category-btn:hover {
  background-color: #4a4d55;
}

.category-btn.active {
  background-color: #912F40;
  color: white;
}

.icon {
  width: 1.25rem;
  height: 1.25rem;
}

.genre-filter {
  margin-bottom: 1.5rem;
}

.genre-title {
  color: #FFFFFF;
  font-size: 1.5rem;
  font-weight: 600;
}

.books-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  width: 100%;
}

.book-card {
  background-color: #3a3d45;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  transition: box-shadow 0.2s, transform 0.2s;
}

.book-card:hover {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
  transform: translateY(-2px);
}

.book-cover-container {
  position: relative;
  overflow: hidden;
}

.book-cover {
  width: 100%;
  height: 18rem;
  object-fit: cover;
}

.overlay {
  position: absolute;
  inset: 0;
  background-color: rgba(0, 0, 0, 0);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s;
}

.book-cover-container:hover .overlay {
  background-color: rgba(0, 0, 0, 0.6);
}

.add-button {
  opacity: 0;
  transition: opacity 0.3s;
  padding: 0.75rem 1.5rem;
  background-color: white;
  color: #912F40;
  border: none;
  border-radius: 0.5rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
  font-weight: 500;
}

.book-cover-container:hover .add-button {
  opacity: 1;
}

.book-info {
  padding: 1.25rem;
}

.book-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.book-text {
  flex: 1;
}

.book-title {
  color: #FFFFFF;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.book-author {
  font-size: 0.875rem;
  color: #9ca3af;
}

.rating-container {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.75rem;
}

.rating {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.star-icon {
  width: 1rem;
  height: 1rem;
  fill: #fbbf24;
  color: #fbbf24;
}

.rating-value {
  color: #FFFFFF;
  font-weight: 500;
}

.reviews {
  font-size: 0.875rem;
  color: #9ca3af;
}

.genre-badge-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.genre-badge {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  background-color: #702632;
  color: #FFFFFF;
  border-radius: 9999px;
  font-size: 0.875rem;
}

@media (max-width: 768px) {
  .books-grid {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1rem;
  }
  
  .category-buttons {
    gap: 0.5rem;
  }
  
  .category-btn {
    padding: 0.5rem 1rem;
    font-size: 0.875rem;
  }
}
</style>