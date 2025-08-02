
<template>
  <section id="library" class="movie-collection">
    <div class="container">
      <!-- Section Title -->
      <div class="header">
        <h1>Movie Collection</h1>
        <!-- Search Box -->
        <div class="search-container">
          <input
            type="text"
            v-model="searchTerm"
            @input="handleSearch"
            placeholder="Search title and add to grid"
            class="search-input"
          >
          <!-- Search Dropdown -->
          <div v-if="searchResults.length > 0" class="search-dropdown">
            <div
              v-for="movie in searchResults"
              :key="movie.id"
              @click="addMovieToGrid(movie)"
              class="search-result-item"
            >
              <div class="result-title">{{ movie.title }}</div>
              <div class="result-overview">{{ movie.overview }}</div>
            </div>
          </div>
          <!-- Loading -->
          <div v-if="loading" class="search-loading">
            Searching...
          </div>
        </div>
      </div>

      <!-- Movie Grid -->
      <div class="moviegrid-content">
        <div
          v-for="movie in movies"
          :key="movie.id"
          class="movie-card"
        >
          <div class="movie-image-container">
            <button
              @click="removeMovie(movie.id)"
              class="close-button"
            >
              ×
            </button>
            <img
              v-if="movie.poster_path"
              :src="movie.poster_path"
              :alt="movie.title"
              class="movie-poster"
            >
            <div v-else class="movie-placeholder">
              <div class="placeholder-content">🎬</div>
            </div>
          </div>
          <div class="movie-info">
            <h3 class="movie-title">{{ movie.title }}</h3>
            <p class="movie-description">{{ movie.overview }}</p>
          </div>
        </div>
      </div>

      <!-- Empty State -->
      <div v-if="movies.length === 0" class="empty-state">
        <div class="empty-icon">🎬</div>
        <h3>No movies in your collection</h3>
        <p>Search and add movies to get started!</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'MovieGrid',
  data() {
    return {
      movies: [],
      searchTerm: '',
      searchResults: [],
      loading: false,
      searchTimeout: null
    };
  },

  async mounted() {
    const ids = [1, 2, 3]; // Static 3 TVmaze show IDs

    try {
      const responses = await Promise.all(
        ids.map(id => fetch(`https://api.tvmaze.com/shows/${id}`))
      );

      const shows = await Promise.all(responses.map(res => res.json()));

      this.movies = shows.map(show => ({
        id: show.id,
        title: show.name,
        overview: show.summary ? show.summary.replace(/<[^>]+>/g, '') : 'No summary available.',
        poster_path: show.image ? show.image.medium : null
      }));
    } catch (err) {
      console.error('Error loading initial shows:', err);
    }
  },

  methods: {
    handleSearch() {
      if (this.searchTimeout) clearTimeout(this.searchTimeout);
      this.searchTimeout = setTimeout(() => {
        this.searchMovies(this.searchTerm);
      }, 300);
    },

    async searchMovies(query) {
      if (!query.trim()) {
        this.searchResults = [];
        return;
      }

      this.loading = true;

      try {
        const response = await fetch(`https://api.tvmaze.com/search/shows?q=${encodeURIComponent(query)}`);
        const data = await response.json();

        this.searchResults = data.slice(0, 5).map(item => {
          const show = item.show;
          return {
            id: show.id,
            title: show.name,
            overview: show.summary ? show.summary.replace(/<[^>]+>/g, '') : 'No summary available.',
            poster_path: show.image ? show.image.medium : null
          };
        });
      } catch (err) {
        console.error('Error searching:', err);
        this.searchResults = [];
      } finally {
        this.loading = false;
      }
    },

    addMovieToGrid(movie) {
      const exists = this.movies.some(m => m.id === movie.id);
      if (!exists) {
        this.movies.push(movie);
      }
      this.searchTerm = '';
      this.searchResults = [];
    },

    removeMovie(id) {
      this.movies = this.movies.filter(movie => movie.id !== id);
    }
  }
};
</script>

<style scoped>
.movie-collection {
  background: #111;
  color: #fff;
  padding: 2rem 0;
}

.container {
  max-width: 1200px;
  margin: auto;
  padding: 0 1rem;
}

.header {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #333;
  padding-bottom: 1rem;
  margin-bottom: 2rem;
}

.header h1 {
  font-size: 2rem;
  font-weight: 500;
}

.search-container {
  position: relative;
  width: 100%;
  max-width: 400px;
}

.search-input {
  width: 100%;
  padding: 0.75rem;
  background: #222;
  color: white;
  border: 1px solid #444;
  border-radius: 4px;
}

.search-dropdown {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: #222;
  border: 1px solid #444;
  z-index: 999;
}

.search-result-item {
  padding: 0.75rem;
  border-bottom: 1px solid #333;
  cursor: pointer;
}

.search-result-item:hover {
  background: #333;
}

.result-title {
  font-weight: bold;
}

.result-overview {
  font-size: 0.85rem;
  color: #ccc;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.search-loading {
  background: #222;
  padding: 0.75rem;
  color: #aaa;
  text-align: center;
}

.moviegrid-content {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

.movie-card {
  background: #1c1c1c;
  border: 1px solid #333;
  border-radius: 6px;
  overflow: hidden;
  position: relative;
}

.close-button {
  position: absolute;
  top: 8px;
  right: 8px;
  background: rgba(0,0,0,0.7);
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  z-index: 2;
}

.movie-image-container {
  height: 500px;
  overflow: hidden;
}

.movie-poster {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.movie-placeholder {
  background: #2a2a2a;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.placeholder-content {
  font-size: 2rem;
  color: #999;
}

.movie-info {
  padding: 1rem;
}

.movie-title {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}

.movie-description {
  font-size: 0.9rem;
  color: #ccc;
  max-height: 3.6em;
  overflow: hidden;
}

.empty-state {
  text-align: center;
  padding: 2rem;
  color: #aaa;
}

.empty-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}
</style>
