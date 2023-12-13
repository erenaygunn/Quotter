<template>
    <header>
        <h1>Quotter</h1>
        <h5>This a public quote platform where you can post and read quotes.</h5>
        <button>Write a Quote</button>
    </header>
</template>

<script>
export default {
    
}
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300;400;500;700&display=swap');

    header {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: 100px;
    }

    header h1 {
        font-size: 5rem;
        font-weight: 700;
        font-family: 'Comfortaa', sans-serif;
        color: #394867;
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
    }
</style>