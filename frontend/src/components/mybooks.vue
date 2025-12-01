<script setup lang="ts">
import { ref } from 'vue';
import { BookOpen, Clock, CheckCircle, Plus } from 'lucide-vue-next';

interface Book {
  id: string;
  title: string;
  author: string;
  cover: string;
  progress: number;
  status: 'reading' | 'want' | 'finished';
}

const activeTab = ref<'reading' | 'want' | 'finished'>('reading');

const myBooks: Book[] = [
  {
    id: '1',
    title: 'O Nome do Vento',
    author: 'Patrick Rothfuss',
    cover: 'https://images.unsplash.com/photo-1544947950-fa07a98d237f?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=400',
    progress: 65,
    status: 'reading',
  },
  {
    id: '2',
    title: '1984',
    author: 'George Orwell',
    cover: 'https://images.unsplash.com/photo-1495446815901-a7297e633e8d?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=400',
    progress: 42,
    status: 'reading',
  },
  {
    id: '3',
    title: 'Sapiens',
    author: 'Yuval Noah Harari',
    cover: 'https://images.unsplash.com/photo-1589998059171-988d887df646?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=400',
    progress: 0,
    status: 'want',
  },
  {
    id: '4',
    title: 'O Hobbit',
    author: 'J.R.R. Tolkien',
    cover: 'https://images.unsplash.com/photo-1621351183012-e2f9972dd9bf?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=400',
    progress: 100,
    status: 'finished',
  },
];

const getFilteredBooks = () => {
  return myBooks.filter(book => book.status === activeTab.value);
};

const getTabCount = (status: 'reading' | 'want' | 'finished') => {
  return myBooks.filter(book => book.status === status).length;
};
</script>

<template>
  <div class="mybooks-container">
    <div class="mybooks-content">
      <h1 class="page-title">Minhas Leituras</h1>

      <div class="tabs-container">
        <button
          @click="activeTab = 'reading'"
          :class="['tab-btn', { active: activeTab === 'reading' }]"
        >
          <BookOpen class="tab-icon" />
          <span>Lendo</span>
          <span class="tab-count">{{ getTabCount('reading') }}</span>
        </button>

        <button
          @click="activeTab = 'want'"
          :class="['tab-btn', { active: activeTab === 'want' }]"
        >
          <Clock class="tab-icon" />
          <span>Quero Ler</span>
          <span class="tab-count">{{ getTabCount('want') }}</span>
        </button>

        <button
          @click="activeTab = 'finished'"
          :class="['tab-btn', { active: activeTab === 'finished' }]"
        >
          <CheckCircle class="tab-icon" />
          <span>Já Li</span>
          <span class="tab-count">{{ getTabCount('finished') }}</span>
        </button>
      </div>

      <div class="books-grid">
        <!-- Card de adicionar livro -->
        <div class="add-book-card">
          <Plus class="add-icon" />
          <p class="add-text">Adicionar Livro</p>
        </div>

        <!-- Cards dos livros -->
        <div v-for="book in getFilteredBooks()" :key="book.id" class="book-card">
          <div class="book-cover-container">
            <img
              :src="book.cover"
              :alt="book.title"
              class="book-cover"
            />
            <div v-if="book.status === 'reading'" class="progress-overlay">
              <span class="progress-text">{{ book.progress }}%</span>
              <div class="progress-bar-container">
                <div 
                  class="progress-bar" 
                  :style="{ width: book.progress + '%' }"
                ></div>
              </div>
            </div>
          </div>
          
          <div class="book-info">
            <h3 class="book-title">{{ book.title }}</h3>
            <p class="book-author">{{ book.author }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.mybooks-container {
  width: 80%;
  background-color: #25272D;
  padding: 2rem 1rem;
  display: flex;
  margin-left: auto;
  min-height: 100vh;
}

.mybooks-content {
  width: 100%;
  max-width: 100%;
  margin: 0 auto;
}

.page-title {
  color: #FFFFFF;
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 2rem;
}

.tabs-container {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2rem;
  border-bottom: 2px solid #3a3d45;
  padding-bottom: 0.5rem;
}

.tab-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: none;
  border: none;
  cursor: pointer;
  transition: all 0.2s;
  color: #9ca3af;
  font-size: 1rem;
  font-weight: 500;
  border-radius: 0.5rem 0.5rem 0 0;
  position: relative;
}

.tab-btn:hover {
  color: #FFFFFF;
  background-color: #3a3d45;
}

.tab-btn.active {
  color: #dc2626;
  background-color: transparent;
}

.tab-btn.active::after {
  content: '';
  position: absolute;
  bottom: -0.6rem;
  left: 0;
  right: 0;
  height: 1px;
  background-color: #dc2626;
  border-radius: 2px;
}

.tab-icon {
  width: 1.25rem;
  height: 1.25rem;
}

.tab-count {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background-color: #3a3d45;
  color: #FFFFFF;
  border-radius: 9999px;
  padding: 0.125rem 0.5rem;
  font-size: 0.875rem;
  min-width: 1.5rem;
  height: 1.5rem;
}

.tab-btn.active .tab-count {
  background-color: #702632;
}

.books-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  width: 100%;
}

.add-book-card {
  background-color: transparent;
  border: 2px dashed #4a4d55;
  border-radius: 0.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s;
  min-height: 400px;
}

.add-book-card:hover {
  border-color: #dc2626;
  background-color: rgba(99, 102, 241, 0.05);
}

.add-icon {
  width: 3rem;
  height: 3rem;
  color: #6b7280;
  margin-bottom: 0.5rem;
}

.add-book-card:hover .add-icon {
  color: #dc2626;
}

.add-text {
  color: #9ca3af;
  font-size: 1rem;
  font-weight: 500;
}

.add-book-card:hover .add-text {
  color: #dc2626;
}

.book-card {
  background-color: #1f2127;
  border-radius: 0.5rem;
  overflow: hidden;
  transition: transform 0.2s, box-shadow 0.2s;
  cursor: pointer;
}

.book-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4);
}

.book-cover-container {
  position: relative;
  width: 100%;
  height: 350px;
  overflow: hidden;
}

.book-cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.progress-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.9), rgba(0, 0, 0, 0.4));
  padding: 1rem;
}

.progress-text {
  color: #FFFFFF;
  font-size: 1.25rem;
  font-weight: 700;
  display: block;
  margin-bottom: 0.5rem;
}

.progress-bar-container {
  width: 100%;
  height: 8px;
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 9999px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, #702632, #dc2626);
  border-radius: 9999px;
  transition: width 0.3s ease;
}

.book-info {
  padding: 1.25rem;
  background-color: #1f2127;
}

.book-title {
  color: #FFFFFF;
  font-weight: 600;
  font-size: 1.125rem;
  margin-bottom: 0.5rem;
  line-height: 1.4;
}

.book-author {
  color: #9ca3af;
  font-size: 0.875rem;
}

@media (max-width: 1024px) {
  .books-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .mybooks-container {
    width: 100%;
    padding: 1rem;
  }

  .tabs-container {
    flex-wrap: wrap;
  }

  .tab-btn {
    font-size: 0.875rem;
    padding: 0.5rem 1rem;
  }

  .page-title {
    font-size: 1.5rem;
  }
}
</style>