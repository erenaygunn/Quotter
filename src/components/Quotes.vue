<template>
    <div class="quotes">
      <Quote v-for="quote in quotes" :key="quote.id" :quote="quote" />
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
        ]
      };
    }
  };
  </script>

<style scoped>
.quotes {
  display: flex;
  padding: 50px 20px 45px 20px;
  margin-top: 50px;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  background-color: #394867;
}

@media screen and (max-width: 425px) {
  .quotes {
    padding: 30px 20px;
  }
}

</style>