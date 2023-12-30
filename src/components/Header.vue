<template>
    <header>
      <h1>Quotter</h1>
      <h5>This is a public quote platform where you can post and read quotes.</h5>
      <button @click="openModal">Write a Quote<Icon icon="jam:write-f" class="icon" /></button>
      <quote-modal :is-open="isModalOpen" @close="closeModal" @submit-quote="handleQuoteSubmission"></quote-modal>
    </header>
  </template>
  
  <script>
  import { Icon } from '@iconify/vue';
  import QuoteModal from './QuoteModal.vue';
  import axios from 'axios';
  
  export default {
    components: {
      Icon,
      QuoteModal,
    },
    data() {
      return {
        isModalOpen: false,
      };
    },
    methods: {
      openModal() {
        this.isModalOpen = true;
      },
      closeModal() {
        this.isModalOpen = false;
      },
      async handleQuoteSubmission(quoteData) {
        try {
            console.log(quoteData)
            // Make an HTTP POST request to save the quote to the database
            const response = await axios.post('http://localhost:3000/api/quotes', quoteData);
            location.reload();

            // Log the response from the server
            console.log('Quote submitted. Server response:', response.data);
        } catch (error) {
            console.error('Error submitting quote:', error);
        }
        },
    },
  };
  </script>
  

<style scoped>
    header {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding-top: 50px;
        text-align: center;
    }

    header h1 {
        font-size: 5rem;
        font-weight: 700;
        font-family: 'Comfortaa', sans-serif;
        color: #212A3E;
    }

    header h5 {
        font-size: 2rem;
        font-weight: 300;
        font-family: 'Ubuntu', sans-serif;
    }

    header button {
        margin-top: 30px;
        font-size: 1.5rem;
        color: #F1F6F9;
        font-family: 'Ubuntu', sans-serif;
        padding: 15px 30px;
        border-radius: 50px;
        border: none;
        background-color: #212A3E;
        display: flex;
        align-items: center;
        transition: all 0.3s;
        position: relative;
        width: 215px;
    }
    header button:hover {
        cursor: pointer;
        width: 250px
    }

    .icon {
        opacity: 0;
        position: absolute;
        padding-left: 10px;
        margin-top: 2px;
        transition: all 0.3s;
        left: 0;
        font-size: 2rem;
    }

    header button:hover .icon {
        opacity: 100%;
        left: 190px;
    }

    @media screen and (max-width: 660px) {
        header {
            margin: 0px 20px 0;
        }

        header h1 {
            font-size: 3rem;
        }

        header h5 {
            font-size: 1.5rem;
        }

        header button {
            width: 250px;
        }

        header button .icon {
        opacity: 100%;
        left: 190px;
    }
    }

    @media screen and (max-width: 425px) {
        header {
            margin: 0px 20px 0;
        }

        header h1 {
            font-size: 2rem;
        }

        header h5 {
            font-size: 1rem;
        }

        header button, header button:hover {
            width: 180px;
            font-size: 1rem;
            white-space: nowrap;
            margin-top: 15px;
        }

        header button .icon, header button:hover .icon {
        left: 125px;
        }

        header button .icon {
            font-size: 1.5rem;
        }
    }
</style>