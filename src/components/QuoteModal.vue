<template>
    <div class="modal-overlay" v-if="isOpen">
      <div class="modal">
        <span class="close-button" @click="closeModal">&times;</span>
        <label for="quote">Quote:</label>
        <textarea v-model="quote" id="quote" rows="4" cols="50"></textarea>
  
        <label for="author">Author:</label>
        <input v-model="author" id="author" type="text" />
  
        <label for="userName">Your Name:</label>
        <input v-model="userName" id="userName" type="text" />
  
        <label for="email">Email:</label>
        <input v-model="email" id="email" type="email" />
  
        <button @click="submitQuote">Submit</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['isOpen'],
    data() {
      return {
        quote: '',
        author: '',
        userName: '',
        email: '',
      };
    },
    methods: {
      closeModal() {
        this.$emit('close');
        this.clearFields();
      },
      submitQuote() {
        // Handle quote submission logic here
        console.log('Quote:', this.quote);
        console.log('Author:', this.author);
        console.log('User Name:', this.userName);
        console.log('Email:', this.email);
  
        // Close the modal after submission
        this.closeModal();
      },
      clearFields() {
        // Clear input fields when the modal is closed
        this.quote = '';
        this.author = '';
        this.userName = '';
        this.email = '';
      },
    },
  };
  </script>
  
  <style scoped>
  .modal-overlay {
    position: fixed;
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
    background: white;
    padding: 20px;
    border-radius: 5px;
    width: 400px;
  }
  
  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 20px;
    cursor: pointer;
  }
  </style>
  