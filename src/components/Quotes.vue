<template>
    <div class="container">
      <div class="search-and-sort">
        <input v-model="searchQuery" type="text" placeholder="Search..." />
        <select v-model="sortOption">
          <option value="date">Sort by Date</option>
          <option value="likes">Sort by Likes</option>
          <option value="length">Sort by Length</option>
        </select>
      </div>
      <div class="quotes">
        <Quote v-for="quote in quotes" :key="quote.id" :quote="quote" />
      </div>
    </div>
</template>
  
  <script>
  import Quote from './Quote.vue';
  
  export default {
    components: {
      Quote
    },
    
    data() {
      return {
        quotes: [
          {
            id: 1,
            text: "The only limit to our realization of tomorrow will be our doubts of today.",
            author: "Franklin D. Roosevelt",
            likes: 42,
            uploader: "Eren",
            date: "21.12.2023"
          },
          {
            id: 1,
            text: "The only limit to our realization of tomorrow will be our doubts of today.",
            author: "Franklin D. Roosevelt",
            likes: 42,
            uploader: "Eren",
            date: "21.12.2023"
          },
          {
            id: 1,
            text: "The only limit to our realization of tomorrow will be our doubts of today.The only limit to our realization of tomorrow will be our doubts of today.The only limit to our realization of tomorrow will be our doubts of today.",
            author: "Franklin D. Roosevelt",
            likes: 42,
            uploader: "Eren",
            date: "21.12.2023"
          },
          {
            id: 1,
            text: "The only limit to our realization of tomorrow will be our doubts of today.",
            author: "Franklin D. Roosevelt",
            likes: 42,
            uploader: "Eren",
            date: "21.12.2023"
          },
          // Add more quotes as needed
        ],
        searchQuery: '',
        sortOption: 'date'
      };
    },

    computed: {
    filteredQuotes() {
      let filtered = [...this.quotes];

      // Search logic
      if (this.searchQuery.trim() !== '') {
        const query = this.searchQuery.toLowerCase();
        filtered = filtered.filter(
          (quote) =>
            quote.text.toLowerCase().includes(query) ||
            quote.author.toLowerCase().includes(query) ||
            quote.uploader.toLowerCase().includes(query)
        );
      }
      // Sorting logic
      switch (this.sortOption) {
        case 'date':
          filtered.sort((a, b) => new Date(b.date) - new Date(a.date));
          break;
        case 'likes':
          filtered.sort((a, b) => b.likes - a.likes);
          break;
        case 'length':
          filtered.sort((a, b) => a.text.length - b.text.length);
          break;
        default:
          break;
      }

      return filtered;

    }
  }
  };
  </script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  margin-top: 50px;
  align-items: center;
}

.quotes {
  display: flex;
  margin: 30px 40px;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  border-radius: 40px;
}


@media screen and (max-width: 425px) {
  .quotes {
    margin: 25px 20px;
  }

  .container {
    margin-top: 30px;
  }
}

</style>