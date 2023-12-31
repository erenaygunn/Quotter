<template>
    <div class="quote">
      <p class="quote-text">{{ quote.quote }}</p>
      <p class="quote-author">- {{ quote.author }}</p>
      <div class="quote-metadata">
        <span class="quote-likes"><button @click="likeQuote" :disabled="quote.isLiked" :class="{ 'liked': quote.isLiked }">
          <Icon icon="iconamoon:like" class="like"/>
        </button> {{ quote.likes }}</span>
        <span class="uploader"> {{ quote.userName }} ~ {{ quote.date }}</span> 
      </div> 
    </div>
    <!-- Modal for entering email -->
    <div v-if="showEmailModal" class="email-modal">
      <div class="email-form">
        <span class="close" @click="showEmailModal = false">&times;</span>
        <label for="email">Enter your email to like the quote</label>
        <input v-model="userEmail" type="email" placeholder="Enter your email" @input="validateEmail" autocomplete="email"/>
        <p v-if="!isValidEmail" class="error-message">Please enter a valid email address.</p>
        <button @click="submitEmail" >Submit</button>
      </div>
    </div>
  </template>
  
<script>
  import { Icon } from '@iconify/vue';
  import axios from 'axios';

  export default {
    components: {
		Icon,
	  },
    props: {
      quote: {
        type: Object,
        required: true
      }
    },
    data() {
    return {
      showEmailModal: false,
      userEmail: '',
      isValidEmail: true,
    }},

    methods: {
      validateEmail() {
      // Simple email validation using a regular expression
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailRegex.test(this.userEmail);
      },

      async likeQuote() {
        if (this.quote.isLiked) {
          return; // Do nothing if the quote is already liked
        }

        // Show the email modal to get the user's email
        this.showEmailModal = true;
      },
      async submitEmail() {
        if (!this.validateEmail()) {
          this.isValidEmail = false;
          return;
        }

        try {
          // Make an HTTP POST request to like the quote with the user's email
          const response = await axios.post('https://quotter-backend.onrender.com/quotes/like', {
            quoteId: this.quote._id,
            userEmail: this.userEmail,
          });

          // Update the quote object with the new like information
          this.quote.likes = response.data.likes;
          this.quote.isLiked = true;

          // Close the email modal
          this.showEmailModal = false;
        } catch (error) {
            // Check if the error is due to reaching the maximum quote limit
            if (error.response && error.response.status === 400) {
                // Inform the user about the maximum quote limit
                window.alert(error.response.data.error);
            } else {
                console.error('Error submitting quote:', error);
            }
            }
      },
  },
  };
</script>
  
<style scoped>
  .error-message {
  color: red;
  margin-top: 5px;
  }

  .quote-likes .liked {
    color: #fff; /* Change the color to your desired color */
  }
  .email-modal {
      position: fixed;
      z-index: 100;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
    }

  .email-form {
    font-family: "Ubuntu", sans-serif;
    position: relative;
    color: #394867;
    white-space: nowrap;
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: #F1F6F9;
    padding: 20px;
    border-radius: 20px;
    margin: 0 10px;
    box-shadow: 10px 8px 30px rgba(255, 255, 255, 0.3);
  }

  .email-form label {
    margin: 25px 0 10px;
    padding-bottom: 10px;
    font-weight: 500;
  }

  .email-form input {
    font-family: "Ubuntu", sans-serif;
    height: 35px;
    border: 1px solid #394867;
    border-radius: 20px;
    padding: 0 20px;
    outline: none;
    color: #212A3E;
  }

  .email-form button {
    font-family: "Ubuntu", sans-serif;
    font-size: 1rem;
    font-weight: 500;
    border: none;
    background-color: #394867;
    color: #F1F6F9;
    margin-top: 15px;
    padding: 12px 18px;
    border-radius: 25px;
    cursor: pointer;
  }

  .close {
    position: absolute;
    top: 5px;
    right: 15px;
    font-size: 30px;
    cursor: pointer;
  }

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
    align-items: center;
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