<script setup lang="ts">
import { ref } from 'vue';
import { BookOpen } from 'lucide-vue-next';

const activeTab = ref('Início');

type ViewType = 'feed' | 'discover' | 'mybooks' | 'community';
const tabs: Array<{ name: string; view: ViewType }> = [
  { name: 'Início', view: 'feed' },
  { name: 'Explorar', view: 'discover' },
  { name: 'Minhas Leituras', view: 'mybooks' },
  { name: 'Comunidade', view: 'community' }
];

const emit = defineEmits<{
  (e: 'viewChange', view: ViewType): void;
}>();

const setActiveTab = (tabName: string, view: ViewType) => {
  activeTab.value = tabName;
  emit('viewChange', view);
};
</script>

<template>
  <header class="header">
    <div class="header-container">
      <div class="logo-section">
        <BookOpen class="logo-icon" />
        <h1 class="logo-text">BookHub</h1>
      </div>

      <nav class="nav-tabs">
        <button
          v-for="tab in tabs"
          :key="tab.name"
          @click="setActiveTab(tab.name, tab.view)"
          :class="['nav-tab', { active: activeTab === tab.name }]"
        >
          {{ tab.name }}
        </button>
      </nav>

      <div class="auth-buttons">
        <button class="btn">Entrar</button>
        <button class="btn">Registrar</button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: linear-gradient(135deg, #912F40 1%, #702632 100%);
  z-index: 100;
}

.header-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 2rem;
  max-width: 1920px;
  margin: 0 auto;
}

.logo-section {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.logo-icon {
  width: 2rem;
  height: 2rem;
  color: #dc2626;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
  margin: 0;
}

.nav-tabs {
  display: flex;
  gap: 0.5rem;
}

.nav-tab {
  padding: 0.625rem 1.25rem;
  background: none;
  border: none;
  color: white;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  border-radius: 1rem;
  transition: all 0.2s;
  position: relative;
}

.nav-tab:hover {
  background-color: #912F40
}

.nav-tab.active {
  background-color: #702632;
}

.nav-tab.active::after {
  content: '';
  position: absolute;
  bottom: -0.5rem;
  left: 0;
  right: 0;
  height: 3px;
  background-color: #702632;
  border-radius: 1rem
}

.auth-buttons {
  display: flex;
  gap: 1rem;
}

.btn {
  padding: 0.625rem 1.5rem;
  border: #702632;
  background: #702632;
  color: white;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 1rem;
  cursor: pointer;
  transition: all 0.2s;
}

.btn:hover {
  background-color: #dc2626;
  transform: translateY(-1px);
}

@media (max-width: 768px) {
  .header-container {
    flex-wrap: wrap;
    padding: 1rem;
  }

  .nav-tabs {
    order: 3;
    width: 100%;
    justify-content: center;
    margin-top: 1rem;
  }

  .nav-tab {
    font-size: 0.875rem;
    padding: 0.5rem 1rem;
  }

  .auth-buttons {
    gap: 0.5rem;
  }

  .btn-entrar,
  .btn {
    padding: 0.5rem 1rem;
    font-size: 0.875rem;
  }
}
</style>