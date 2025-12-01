<script setup lang="ts">
import { ref } from 'vue';
import headerBH from './components/headerBH.vue';
import sidebarBH from './components/sidebarBH.vue';
import footerBH from './components/footerBH.vue';
import feed from './components/feed.vue';
import discover from './components/discover.vue';
import mybooks from './components/mybooks.vue';

const selectedGenre = ref<string | null>(null);
const currentView = ref<'feed' | 'mybooks' | 'discover' | 'community'>('feed');

const handleGenreSelect = (genre: string | null) => {
  selectedGenre.value = genre;
};

const handleViewChange = (view: 'feed' | 'mybooks' | 'discover' | 'community') => {
  currentView.value = view;
};
</script>

<template>
  <div class="app-wrapper">
    <headerBH @viewChange="handleViewChange" />
    <router-view />
    
    <div class="content-container">
      <sidebarBH 
        class="sidebar"
        :selectedGenre="selectedGenre"
        @genreSelect="handleGenreSelect"
        @viewChange="handleViewChange"
      />
      
      <main class="main-content">
        <!-- Renderização condicional baseada na view atual -->
        <feed v-if="currentView === 'feed'" />
        <discover v-else-if="currentView === 'discover'" :selectedGenre="selectedGenre" />
        
        <!-- Adicionar outros componentes conforme necessário -->
        <mybooks v-else-if="currentView === 'mybooks'" :selectedGenre="selectedGenre"/>
        
        <div v-else-if="currentView === 'community'">
          <h2>Comunidade (em construção)</h2>
        </div>
      </main>
    </div>

    <footerBH />
  </div>
</template>

<style scoped>
.app-wrapper {
  min-height: 100%;
  display: flex;
  flex-direction: column;
  background-color: #25272D;
}

.sidebar{
  display: inline;
  margin-top: 4rem;
}

.content-container {
  display: flex;
  flex: 1;
  margin-top: 3.5rem;
}

.main-content {
  flex: 1;
  padding: 1rem;
  overflow-y: auto;
}

@media (max-width: 768px) {
  .content-container {
    flex-direction: column;
    margin-top: 60px;
  }
  
  .main-content {
    padding: 1rem;
  }
}
</style>