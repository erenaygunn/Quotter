<template>
  <div class="modal-overlay" v-if="isOpen">
    <div class="modal">
      <span class="close" @click="closeModal">&times;</span>
      <form @submit.prevent="submitQuote">
        <ul>
          <li>
            <label for="quote">Quote:</label>
            <textarea v-model="quote" id="quote" required @input="validateQuote"></textarea>
            <p class="error-message">{{ quoteError }}</p>
          </li>
          <li>
            <label for="author">Author:</label>
            <input v-model="author" type="text" id="author" required/>
          </li>
          <li>
            <label for="userName">Your Name (Optional):</label>
            <input v-model="userName" type="text" id="userName" autocomplete="given-name"/>
          </li>
          <li>
            <label for="email">Email:</label>
            <input v-model="email" type="email" id="email" required autocomplete="email"/>
          </li>
          <button type="submit" class="submit">Publish</button>
        </ul>
      </form>
    </div>
  </div>
</template>
  
  <script>
  export default {
    props: ['isOpen'],
    data() {
      return {
          quoteData: {
          quote: '',
          author: '',
          likes: 0,
          userName: '',
          email: '',
          date: '',
        },
        quote: '',
        author: '',
        userName: '',
        email: '',
        quoteError: '',
      };
    },
    methods: {
      closeModal() {
        this.$emit('close');
      },

      submitQuote() {
        if (
          this.quote.length < 25
        ) {
          window.alert("Quote must be at least 25 characters length.")
          return;
        }

        if (this.author.length > 24) {
          window.alert('Author name must be 24 characters or less.');
          return;
        }

        // Validate Username Length
        if (this.userName.length > 24) {
          window.alert('Username must be 24 characters or less.');
          return;
        }
        
         // Update quoteData before emitting the event
        this.quoteData = {
        quote: this.quote,
        author: this.author,
        likes: 0,
        userName: this.userName,
        email: this.email,
        date: "0",
        }

        this.$emit('submit-quote', this.quoteData);
        console.log(this.quoteData)
        console.log('Quote:', this.quote);
        console.log('Author:', this.author);
        console.log('User Name:', this.userName);
        console.log('Email:', this.email);
        // Close the modal after submission
        this.clearFields()
        this.clearData
        this.closeModal();
        
        },

      validateQuote() {
      this.quoteError = this.quote.length < 25 ? 'Quote must be at least 25 characters.' : '';
      },

      clearData() {
        this.quoteData = {
          quote: '',
          author: '',
          userName: '',
          email: '',
        };
      },
      clearFields() {
        this.quote = '';
        this.author = '';
        this.userName = '';
        this.email = '';
      }
    },
  };
  </script>
  
  <style scoped>

  .error-message {
    color: red;
    margin-top: 5px;
    font-size: 12px;
  }
  .modal-overlay {
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
  
  .modal {
    font-family: "Ubuntu", sans-serif;
    position: relative;
    color: #394867;
    white-space: nowrap;
    display: flex;
    justify-content: center;
    background: #F1F6F9;
    padding: 20px;
    border-radius: 20px;
    margin: 0 10px;
    box-shadow: 10px 8px 30px rgba(255, 255, 255, 0.3);
  }
  
  .close {
    position: absolute;
    top: 5px;
    right: 15px;
    font-size: 30px;
    cursor: pointer;
  }

  .modal form ul{
    list-style-type: none;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .modal form ul li {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin: 10px;
  }

  .modal form ul li label {
    padding-bottom: 10px;
    font-weight: 500;
  }

  .modal form ul li textarea {
    font-family: "Ubuntu", sans-serif;
    border-radius: 20px;
    padding: 10px 20px;
    outline: none;
    border: 1px solid #394867;
    color: #212A3E;
    resize: none;
    width: 224px;
    height: 100px;
  }

  textarea::-webkit-scrollbar {
    width: 1em;
    padding-right: 50px;
  }

  textarea::-webkit-scrollbar-track {
      -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
  }

  textarea::-webkit-scrollbar-thumb {
    background-color: darkgrey;
    outline: 1px solid slategrey;
  }

  .modal form ul li input {
    font-family: "Ubuntu", sans-serif;
    height: 35px;
    border: 1px solid #394867;
    border-radius: 20px;
    padding: 0 20px;
    outline: none;
    color: #212A3E;
  }

  .modal .submit {
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

  @media screen and (min-width: 426px) {
    .modal, .modal input, .modal textarea {
      font-size: 1.2rem;
    }

    .modal input, .modal form ul li textarea {
      width: 302px;
    }

    .modal form ul li input {
      height: 45px;
    }

    .modal form ul li textarea {
      height: 150px;
    }

    .modal .submit {
      font-size: 1.2rem;
    }
  }

  @media screen and (min-width: 1441px) {
    .modal, .modal input, .modal textarea {
      font-size: 1.5rem;
    }

    .modal input, .modal form ul li textarea {
      width: 450px;
    }

    .modal form ul li input {
      height: 50px;
    }

    .modal form ul li textarea {
      height: 170px;
    }
  }

  </style>
  