<template>
    <div class="quote">
      <p class="quote-text">{{ quote.text }}</p>
      <p class="quote-author">- {{ quote.author }}</p>
      <div class="quote-metadata">
        <span class="quote-likes"><button>
          <Icon icon="iconamoon:like" class="like"/>
        </button> {{ quote.likes }}</span>
        <span class="uploader"> {{ quote.uploader }} ~ {{ quote.date }}</span>
        
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
    justify-content: space-around;
    padding: 30px;
    background-color: #212A3E;
    border-radius: 30px;
    margin: 0 20px 20px 20px;
    max-width: 500px;
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
    flex-direction: row;
    justify-content: space-between;
    color: #9BA4B5;
    font-family: 'Ubuntu', sans-serif;
    white-space: nowrap;
  }

  .quote-likes {
    display: flex;
    align-items: center;
    padding-right: 5px;
  }
  .quote-likes button {
    padding: 6px 3px 0 0;
    background: none;
    border: none;
    color: #9BA4B5;
    font-size: 1.2rem;
  }

  .quote-likes button:hover {
    cursor: pointer;
    color: #F1F6F9;
  }

  @media screen and (max-width: 425px) {
    .quote {
      margin: 0 10px 10px 10px;
    }
    .quote-text, .quote-author, .quote-metadata {
        font-size: 0.8rem;
    }

    .quote-metadata {
      flex-wrap: wrap;
    }

    .quote-likes button {
      font-size: 1rem;
    }
  }
  
  </style>