<script setup lang="ts">
import { ref } from 'vue';
import { Heart, MessageCircle, Share2, Star } from 'lucide-vue-next';

interface Post {
  id: string;
  user: {
    name: string;
    avatar: string;
  };
  type: 'review' | 'status' | 'recommendation';
  book: {
    title: string;
    author: string;
    cover: string;
  };
  content: string;
  rating?: number;
  likes: number;
  comments: number;
  timestamp: string;
  liked: boolean;
}

const mockPosts: Post[] = [
  {
    id: '1',
    user: {
      name: 'Maria Silva',
      avatar: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=100&h=100&fit=crop',
    },
    type: 'review',
    book: {
      title: 'O Nome do Vento',
      author: 'Patrick Rothfuss',
      cover: 'https://images.unsplash.com/photo-1711185892188-13f35959d3ca?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    },
    content: 'Uma obra-prima da fantasia moderna! A narrativa é envolvente do início ao fim. Rothfuss criou um mundo rico e personagens inesquecíveis. Mal posso esperar para ler o próximo.',
    rating: 5,
    likes: 42,
    comments: 8,
    timestamp: 'há 2 horas',
    liked: false,
  },
  {
    id: '2',
    user: {
      name: 'João Costa',
      avatar: 'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?w=100&h=100&fit=crop',
    },
    type: 'status',
    book: {
      title: '1984',
      author: 'George Orwell',
      cover: 'https://images.unsplash.com/photo-1534289855405-ab820a118fc1?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    },
    content: 'Comecei a ler hoje. Já estou impressionado com a atualidade das questões levantadas por Orwell.',
    likes: 15,
    comments: 3,
    timestamp: 'há 5 horas',
    liked: true,
  },
  {
    id: '3',
    user: {
      name: 'Ana Paula',
      avatar: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=100&h=100&fit=crop',
    },
    type: 'recommendation',
    book: {
      title: 'Sapiens',
      author: 'Yuval Noah Harari',
      cover: 'https://images.unsplash.com/photo-1568667256531-7d5ac92eaa7a?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
    },
    content: 'Para quem gosta de história e antropologia, este livro é imperdível! Uma jornada fascinante pela história da humanidade.',
    rating: 5,
    likes: 67,
    comments: 12,
    timestamp: 'há 1 dia',
    liked: false,
  },
];

const posts = ref<Post[]>(mockPosts);
const newPostContent = ref('');

const toggleLike = (postId: string) => {
  posts.value = posts.value.map(post => {
    if (post.id === postId) {
      return {
        ...post,
        liked: !post.liked,
        likes: post.liked ? post.likes - 1 : post.likes + 1,
      };
    }
    return post;
  });
};
</script>

<template>
  <div class="feed-container">
    <div class="posts-wrapper">
      <!-- Nova publicação -->
      <div class="new-post-card">
        <textarea
          v-model="newPostContent"
          placeholder="Compartilhe suas impressões sobre um livro..."
          class="new-post-textarea"
          rows="3"
        />
        <div class="new-post-actions">
          <button class="btn">
            Publicar
          </button>
        </div>
      </div>

      <!-- Posts -->
      <div v-for="post in posts" :key="post.id" class="post-card">
        <div class="post-wrapper">
          <img
            :src="post.user.avatar"
            :alt="post.user.name"
            class="user-avatar"
          />
          <div class="post-content">
            <div class="post-header">
              <div>
                <p class="user-name">{{ post.user.name }}</p>
                <p class="post-timestamp">{{ post.timestamp }}</p>
              </div>
              <div v-if="post.type === 'review'" class="stars-container">
                <Star
                  v-for="i in 5"
                  :key="i"
                  :class="[
                    'star-icon',
                    i <= (post.rating || 0) ? 'star-filled' : 'star-empty'
                  ]"
                />
              </div>
            </div>

            <div class="book-section">
              <img
                :src="post.book.cover"
                :alt="post.book.title"
                class="book-cover"
              />
              <div class="book-details">
                <p class="book-title">{{ post.book.title }}</p>
                <p class="book-author">{{ post.book.author }}</p>
                <p class="post-text">{{ post.content }}</p>
              </div>
            </div>

            <div class="post-actions">
              <button
                @click="toggleLike(post.id)"
                :class="['action-button', { 'action-liked': post.liked }]"
              >
                <Heart :class="['icon', { 'heart-filled': post.liked }]" />
                <span>{{ post.likes }}</span>
              </button>
              <button class="action-button">
                <MessageCircle class="icon" />
                <span>{{ post.comments }}</span>
              </button>
              <button class="action-button">
                <Share2 class="icon" />
                <span>Compartilhar</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.feed-container {
  max-width: 80%;
  display: flex;
  margin-left: auto;
  padding: 1rem;
  gap: 1rem;
  
}

.posts-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.new-post-card {
  background-color: #40434E;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
}

.new-post-textarea {
  width: 100%;
  background-color: #40434E;
  padding: 1rem;
  border: 1px solid #e5e7eb;
  color: white;
  border-radius: 0.5rem;
  resize: none;
  font-family: inherit;
  font-size: 1rem;
}

.new-post-textarea:focus {
  outline: none;
  border-color: #e5e7eb;
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
}

.new-post-actions {
  display: flex;
  justify-content: flex-end;
  margin-top: 1rem;
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

.post-card {
  background-color: #40434E;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
}

.post-wrapper {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.user-avatar {
  width: 3rem;
  height: 3rem;
  border-radius: 9999px;
  object-fit: cover;
  flex-shrink: 0;
}

.post-content {
  flex: 1;
}

.post-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.user-name {
  color: #ffffff;
  font-weight: 600;
  font-size: 1rem;
}

.post-timestamp {
  font-size: 0.875rem;
  color: #ffffff;
  margin-top: 0.125rem;
}

.stars-container {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.star-icon {
  width: 1rem;
  height: 1rem;
}

.star-filled {
  fill: #fbbf24;
  color: #fbbf24;
}

.star-empty {
  color: #d1d5db;
}

.book-section {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.book-cover {
  width: 6rem;
  height: 8rem;
  object-fit: cover;
  border-radius: 0.25rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  flex-shrink: 0;
}

.book-details {
  flex: 1;
}

.book-title {
  color: #ffffff;
  font-weight: 600;
  margin-bottom: 0.25rem;
  font-size: 1rem;
}

.book-author {
  font-size: 0.875rem;
  color: #ffffff;
  margin-bottom: 0.75rem;
}

.post-text {
  color: #ffffff;
  line-height: 1.5;
  font-size: 0.938rem;
}

.post-actions {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #f3f4f6;
}

.action-button {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: none;
  border: none;
  color: #ffffff;
  cursor: pointer;
  transition: color 0.2s;
  font-size: 0.938rem;
  padding: 0;
}

.action-button:hover {
  color: #dc2626;
}

.action-button.action-liked {
  color: #ef4444;
}

.action-button.action-liked:hover {
  color: #dc2626;
}

.icon {
  width: 1.25rem;
  height: 1.25rem;
}

.heart-filled {
  fill: #ef4444;
}
</style>