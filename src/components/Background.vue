<template>
    <div class="bullet-main">
        <div class="bullet1 stylebullet"></div>
        <div class="bullet2 stylebullet"></div>
        <div class="bullet3 stylebullet"></div>
        <div class="bullet4 stylebullet"></div>
        <div class="bullet5 stylebullet"></div>
        <div class="bullet6 stylebullet"></div>
        <div class="bullet7 stylebullet"></div>
        <div class="bullet8 stylebullet"></div>
        <div class="bullet9 stylebullet"></div>
        <div class="bullet10 stylebullet"></div>
        <div class="bullet11 stylebullet"></div>
        <div class="bullet12 stylebullet"></div>
        <div class="bullet13 stylebullet"></div>
        <div class="bullet14 stylebullet"></div>
        <div class="bullet15 stylebullet"></div>
    </div>
</template>

<script>
export default {
    
}
</script>
<style >
.bullet-main {
    z-index: -99;
    position: fixed;
    bottom: 0px;
    height: 30px;
    width: 30px;

}

.stylebullet {
    position: absolute;
    overflow: hidden;
    border-radius: 50%;
    height: 30px;
    width: 30px;
    margin-bottom: 0px;
    animation: bullets 20s infinite linear;
    opacity: 0%;
    box-shadow: inset -7px -7px 0 10px #394867;
}

.bullet1 {
    margin-bottom: -5px;
    margin-left: 800px;
    scale: 0.8;
}

.bullet2 {
    margin-bottom: -60px;
    margin-left: 900px;
    scale: 1.2;
    animation-delay: 9000ms;
}

.bullet3 {
    margin-bottom: 150px;
    margin-left: 1000px;
    scale: .9;
    animation-delay: 1000ms;
}

.bullet4 {
    margin-bottom: 20px;
    margin-left: 1100px;
    scale: 1.4;
    animation-delay: 3000ms;
}

.bullet5 {
    margin-bottom: -50px;
    margin-left: 1200px;
    scale: 1;
    animation-delay: 5000ms;
}

.bullet6 {
    margin-bottom: 0px;
    margin-left: 1300px;
    scale: .5;
    animation-delay: 2000ms;
}

.bullet7 {
    margin-bottom: -25px;
    margin-left: 1500px;
    scale: .9;
    animation-delay: 10000ms;
}

.bullet8 {
    margin-bottom: 100px;
    margin-left: 1600px;
    scale: 1.1;
    animation-delay: 0ms;
}

.bullet9 {
    margin-bottom: 30px;
    margin-left: 1700px;
    scale: 1.5;
    animation-delay: 3000ms;
}

.bullet10 {
    margin-bottom: -90px;
    margin-left: 200px;
    scale: .8;
    animation-delay: 7000ms;
}

.bullet11 {
    margin-bottom: 40px;
    margin-left: 300px;
    scale: .9;
    animation-delay: 4000ms;
}

.bullet12 {
    margin-bottom: -120px;
    margin-left: 400px;
    scale: 1.6;
    animation-delay: 3500ms;
}

.bullet13 {
    margin-bottom: 20px;
    margin-left: 500px;
    scale: 1.2;
    animation-delay: 12000ms;
}

.bullet14 {
    margin-bottom: 50px;
    margin-left: 600px;
    scale: 1;
    animation-delay: 2500ms;
}

.bullet15 {
    margin-bottom: 70px;
    margin-left: 700px;
    scale: .4;
    animation-delay: 6000ms;
}

@keyframes bullets {
    0% {
        opacity: 0%;
        bottom: 0px;    
    }
    100% {
        opacity: 70%;
        bottom: 120vh;
    }
}
</style>