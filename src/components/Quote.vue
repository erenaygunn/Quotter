<template>
    <div class="quote">
      <p class="quote-text">{{ quote.text }}</p>
      <p class="quote-author">- {{ quote.author }}</p>
      <div class="quote-metadata">
        <span class="quote-likes">Likes: {{ quote.likes }}</span>
        <span class="uploader">By {{ quote.uploader }}</span>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      quote: {
        type: Object,
        required: true
      }
    }
  };
  </script>
  
  <style scoped>
  .quote {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: #394867;
    border-radius: 30px;
    margin: 30px;
  }
  
  .quote-text {
    font-size: 1.2rem;
    margin-bottom: 5px;
    color: #F1F6F9;
    font-family: 'Comfortaa', sans-serif;
  }
  
  .quote-author {
    font-style: italic;
    color: #9BA4B5;
    margin-bottom: 10px;
    font-family: 'Ubuntu', sans-serif;
  }
  
  .quote-metadata {
    display: flex;
    justify-content: space-between;
    color: #9BA4B5;
    font-family: 'Ubuntu', sans-serif;
  }

  @media screen and (max-width: 380px) {
    .quote-text, .quote-author, .quote-metadata {
        font-size: 0.8rem;
    }
  }
  
  </style>