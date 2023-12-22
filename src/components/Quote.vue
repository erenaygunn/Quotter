<template>
    <div class="quote">
      <p class="quote-text">{{ quote.text }}</p>
      <p class="quote-author">- {{ quote.author }}</p>
      <div class="quote-metadata">
        <span class="quote-likes"><Icon icon="iconamoon:like" class="like"/> {{ quote.likes }}</span>
        <span class="uploader">{{ quote.date }} ~ {{ quote.uploader }}</span>
        
      </div>
    </div>
  </template>
  
<script>
  import { Icon } from '@iconify/vue';

  export default {
    components: {
		Icon,
	  },
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

  .quote-likes {
    display: flex;
    align-items: center;
  }
  .quote-likes .like {
    padding: 2px 3px 0 0;
  }

  @media screen and (max-width: 380px) {
    .quote-text, .quote-author, .quote-metadata {
        font-size: 0.8rem;
    }
  }
  
  </style>