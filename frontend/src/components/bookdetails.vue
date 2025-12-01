<script setup lang="ts">
import { ref } from 'vue';
import { Star } from 'lucide-vue-next';

interface Review {
  id: string;
  author: string;
  rating: number;
  comment: string;
  date: string;
}

const userRating = ref(0);
const hoverRating = ref(0);
const reviewText = ref('');

const book = {
  title: 'O Nome do Vento',
  author: 'Patrick Rothfuss',
  rating: 4.5,
  totalRatings: 5,
  cover: 'https://images.unsplash.com/photo-1711185892188-13f35959d3ca?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=300',
  description: 'A história de Kvothe, um personagem lendário que é herói e vilão, mago e músico, assassino e salvador. Esta é a sua história contada por ele mesmo.',
};

const reviews: Review[] = [
  {
    id: '1',
    author: 'Maria Silva',
    rating: 5,
    comment: 'Simplesmente fantástico! Uma das melhores fantasias que já li. Rothfuss constrói um mundo incrível com uma prosa poética que te transporta para dentro da história.',
    date: '12/08/2023',
  },
  {
    id: '2',
    author: 'João Santos',
    rating: 4,
    comment: 'Ótimo livro, personagens bem construídos e mundo rico. Só não dei 5 estrelas porque acho que o ritmo em alguns momentos é um pouco lento.',
    date: '05/08/2023',
  },
];

const setRating = (rating: number) => {
  userRating.value = rating;
};

const handleMouseEnter = (rating: number) => {
  hoverRating.value = rating;
};

const handleMouseLeave = () => {
  hoverRating.value = 0;
};

const submitReview = () => {
  console.log('Enviando avaliação:', {
    rating: userRating.value,
    text: reviewText.value,
  });
};
</script>

<template>
  <div class="book-details-container">
    <div class="book-info-card">
      <div class="book-content">
        <img
          :src="book.cover"
          :alt="book.title"
          class="book-cover"
        />

        <div class="book-info">
          <h1 class="book-title">{{ book.title }}</h1>
          <p class="book-author">{{ book.author }}</p>

          <div class="rating-display">
            <Star
              v-for="i in 5"
              :key="i"
              :class="[
                'star-icon',
                i <= Math.floor(book.rating) ? 'star-filled' : 
                i <= book.rating ? 'star-half' : 'star-empty'
              ]"
            />
            <span class="rating-text">{{ book.rating }}/5</span>
          </div>

          <p class="book-description">
            {{ book.description }}
          </p>

          <button class="want-read-btn">
            Quero Ler
          </button>
        </div>
      </div>
    </div>

    <div class="reviews-card">
      <h2 class="reviews-title">Avaliações</h2>

      <div class="reviews-list">
        <div
          v-for="review in reviews"
          :key="review.id"
          class="review-item"
        >
          <div class="review-header">
            <div>
              <p class="review-author">{{ review.author }}</p>
              <p class="review-date">{{ review.date }}</p>
            </div>
            <div class="review-stars">
              <Star
                v-for="i in 5"
                :key="i"
                :class="[
                  'star-small',
                  i <= review.rating ? 'star-filled' : 'star-empty'
                ]"
              />
            </div>
          </div>
          <p class="review-comment">{{ review.comment }}</p>
        </div>
      </div>

      <div class="new-review-section">
        <h3 class="new-review-title">Deixe sua avaliação</h3>
        
        <textarea
          v-model="reviewText"
          placeholder="Compartilhe sua opinião sobre este livro..."
          class="review-textarea"
          rows="4"
        />

        <div class="review-actions">
          <div class="rating-input">
            <span class="rating-label">Sua avaliação:</span>
            <div class="rating-stars">
              <button
                v-for="i in 5"
                :key="i"
                @click="setRating(i)"
                @mouseenter="handleMouseEnter(i)"
                @mouseleave="handleMouseLeave"
                class="star-button"
                type="button"
              >
                <Star
                  :class="[
                    'star-interactive',
                    i <= (hoverRating || userRating) ? 'star-filled' : 'star-empty'
                  ]"
                />
              </button>
            </div>
          </div>

          <button @click="submitReview" class="submit-btn">
            Enviar Avaliação
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.book-details-container {
  max-width: 56rem;
  margin: 0 auto;
}

.book-info-card {
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  padding: 2rem;
  margin-bottom: 1.5rem;
}

.book-content {
  display: flex;
  gap: 2rem;
}

.book-cover {
  width: 12rem;
  height: 18rem;
  object-fit: cover;
  border-radius: 0.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  flex-shrink: 0;
}

.book-info {
  flex: 1;
}

.book-title {
  color: #111827;
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.book-author {
  color: #374151;
  font-size: 1.125rem;
  margin-bottom: 1rem;
}

.rating-display {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.star-icon {
  width: 1.25rem;
  height: 1.25rem;
}

.star-filled {
  fill: #fbbf24;
  color: #fbbf24;
}

.star-half {
  fill: #fde68a;
  color: #fbbf24;
}

.star-empty {
  color: #d1d5db;
}

.rating-text {
  color: #111827;
  margin-left: 0.5rem;
  font-weight: 600;
}

.book-description {
  color: #374151;
  line-height: 1.75;
  margin-bottom: 1.5rem;
}

.want-read-btn {
  color: #4f46e5;
  background: none;
  border: none;
  cursor: pointer;
  font-weight: 500;
  transition: color 0.2s;
}

.want-read-btn:hover {
  color: #4338ca;
}

.reviews-card {
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  padding: 2rem;
}

.reviews-title {
  color: #111827;
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
}

.reviews-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.review-item {
  border-bottom: 1px solid #e5e7eb;
  padding-bottom: 1.5rem;
}

.review-item:last-child {
  border-bottom: none;
}

.review-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 0.75rem;
}

.review-author {
  color: #111827;
  font-weight: 600;
}

.review-date {
  font-size: 0.875rem;
  color: #6b7280;
  margin-top: 0.25rem;
}

.review-stars {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.star-small {
  width: 1rem;
  height: 1rem;
}

.review-comment {
  color: #374151;
  line-height: 1.625;
}

.new-review-section {
  border-top: 1px solid #e5e7eb;
  padding-top: 2rem;
}

.new-review-title {
  color: #111827;
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.review-textarea {
  width: 100%;
  padding: 1rem;
  border: 1px solid #d1d5db;
  border-radius: 0.5rem;
  resize: none;
  font-family: inherit;
  margin-bottom: 1rem;
}

.review-textarea:focus {
  outline: none;
  border-color: #4f46e5;
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
}

.review-actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.rating-input {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.rating-label {
  color: #374151;
  font-weight: 500;
}

.rating-stars {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.star-button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  transition: transform 0.2s;
}

.star-button:hover {
  transform: scale(1.1);
}

.star-interactive {
  width: 1.5rem;
  height: 1.5rem;
}

.submit-btn {
  padding: 0.5rem 1.5rem;
  background-color: #4f46e5;
  color: white;
  border: none;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: background-color 0.2s;
  font-weight: 500;
}

.submit-btn:hover {
  background-color: #4338ca;
}
</style>