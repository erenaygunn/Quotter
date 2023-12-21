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
    background-color: #212A3E;
    border-radius: 30px;
    margin: 30px;
  }
  
  .quote-text {
    font-size: 18px;
    margin-bottom: 5px;
    color: #F1F6F9;
  }
  
  .quote-author {
    font-style: italic;
    color: #9BA4B5;
    margin-bottom: 10px;
  }
  
  .quote-metadata {
    display: flex;
    justify-content: space-between;
    color: #9BA4B5;
  }
  
  </style>