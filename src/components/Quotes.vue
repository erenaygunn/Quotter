<template>
    <div class="container">

      <div class="search-and-sort">

        <div class="search-bar">
          <input v-model="searchQuery" type="text" placeholder="Search..." id="search" autocomplete="off"/>
          <Icon icon="ri:search-line" class="search-icon"/>
        </div>

        <div class="sort-dropdown" :class="{ 'active': showSortDropdown }">
          <button @click="toggleSortDropdown">
            <Icon icon="ic:sharp-sort" />
          </button>
          <div v-show="showSortDropdown" class="sort-options">
            <p @click="changeSortOption('date')">Sort by Date</p>
            <p @click="changeSortOption('likes')">Sort by Likes</p>
            <p @click="changeSortOption('length')">Sort by Length</p>
          </div>
        </div>

      </div>
      <div class="quotes">
        <div v-if="quotes.length === 0" class="loading-icon">
          <Spinner/>
        </div>
        <Quote v-for="quote in filteredQuotes" :key="quote.id" :quote="quote" />
      </div>
    </div>
</template>
  
  <script>
  import Quote from './Quote.vue';
  import Spinner from './Spinner.vue';
  import { Icon } from '@iconify/vue';
  import axios from 'axios';
  
  
  export default {
    components: {
      Quote,
      Icon,
      Spinner
    },
    
    data() {
      return {
        quotes: [],
        searchQuery: '',
        sortOption: 'date',
        showSortDropdown: false,
      };
    },

    async created() {
    this.quotes = await this.fetchQuotes();
    },

    methods: {
      async fetchQuotes() {
        try {
          const response = await axios.get('https://quotter-backend.onrender.com/api/quotes');
          return response.data;
        } catch (error) {
          console.error('Error fetching quotes:', error);
          return []; // Return an empty array in case of an error
        }
      },
      toggleSortDropdown() {
      this.showSortDropdown = !this.showSortDropdown;
      },
      changeSortOption(option) {
        this.sortOption = option;
        this.showSortDropdown = false;
      }
    
    },

    computed: {
      filteredQuotes() {
        let filtered = [...this.quotes];

        // Search logic
        if (this.searchQuery.trim() !== '') {
          const query = this.searchQuery.toLowerCase();
          filtered = filtered.filter((quote) => {
            // Check if the properties exist before using toLowerCase()
            const quoteText = quote.quote ? quote.quote.toLowerCase() : '';
            const author = quote.author ? quote.author.toLowerCase() : '';
            const uploader = quote.userName ? quote.userName.toLowerCase() : '';

            return (
              quoteText.includes(query) || author.includes(query) || uploader.includes(query)
            );
          });
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
          filtered.sort((a, b) => a.quote.length - b.quote.length);
          break;
        default:
          break;
      }

      return filtered;
    }
  },
  mounted() {
    this.fetchQuotes(); 
  },

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
  margin: 70px 30px 40px;
  flex-wrap: wrap;
  justify-content: center;
  border-radius: 40px;
}

.search-and-sort {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: 'Ubuntu', sans-serif;
}
.search-and-sort .search-bar{
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #212A3E;
}

.search-and-sort .search-bar .search-icon {
  position: relative;
  right: 30px;
  color: #394867;
}

.search-and-sort input {
  padding: 10px 20px;
  border: 1px solid #394867;
  border-radius: 25px;
  outline: none;
  font-family: 'Ubuntu', sans-serif;
  background-color: #fff;
  width: 200px;
  color: #394867;
}

.search-and-sort input::placeholder {
  color: #9BA4B5;
}

.sort-dropdown {
  position: relative;
}

.sort-dropdown button {
  background: transparent;
  border: 1px solid transparent;
  font-size: 1.5rem;
  padding: 6px 6px 0;
  color: #394867;
  border-radius: 50px;
  transition: all 0.3s;
}

.sort-dropdown button:hover, .sort-dropdown.active button {
  background-color: #fff;
  cursor: pointer;
  border-color: #394867;
}

.sort-options {
  color: #394867;
  position: absolute;
  top: 100%;
  right: 0;
  background-color: #fff;
  border-radius: 25px;
  padding: 15px 10px;
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  z-index: 1;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  white-space: nowrap;
}

.sort-options p {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 7px 7px 0 7px;
  padding-bottom: 10px;
  border-bottom: 1px solid #9BA4B5;
}

.sort-options p:hover {
  cursor: pointer;
}

.sort-options p:last-child {
  border-bottom: none; /* Remove border for the last item */
}

@media screen and (max-width: 425px) {
  .quotes {
    margin: 25px 20px;
  }

  .container {
    margin-top: 30px;
  }
}

@media screen and (min-width: 426px) {
  .search-and-sort input {
    width: 300px;
    height: 50px;
    font-size: 1rem;
  }
}

@media screen and (min-width: 1441px) {
  .search-and-sort input {
    width: 450px;
    height: 55px;
    font-size: 1.2rem;
  }

  .sort-dropdown button {
    font-size: 2rem;
  }

  .search-and-sort .search-bar .search-icon {
    font-size: 1.5rem;
    right: 45px;
  }
}

</style>