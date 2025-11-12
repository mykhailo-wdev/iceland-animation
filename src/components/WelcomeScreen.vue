<template>
    <main class="wrapper">
        <section  ref="layer" class="layer">
            <div class="texts">
                <div class="title">
                    <h1>Розпочніть подорож в</h1>
                    <p class="content">
                        <span class="accent accent-stroke">Ісландію</span><br/>
                        <span class="accent accent-wave">Ісландію</span><br/>
                    </p>
                    <p>прямо зараз</p>
                </div>
            </div>
            <img src="/images/plane.webp" alt="An airplane symbolizing a trip to Iceland" class="plane">
        </section>
        <div class="bg bg-1"></div>
        <section class="welcome-block">
            <p class="welcome-text">
                Welcome to
                <span class="transparent-text">Iceland</span>
            </p>
        </section>
        <div class="bg bg-2"></div>
    </main>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const layer = ref<null | HTMLElement>(null);

const movePlane = () => {
    const scrollY = window.scrollY;
    if(layer.value) {
        layer.value.style.left = `${scrollY}px`;
    }
}

onMounted(() => {
    window.addEventListener('scroll', movePlane);
}) 

onUnmounted(() => {
    window.removeEventListener('scroll', movePlane);
}) 

</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.wrapper {
    font-family: "Poppins", sans-serif;
    color: $palette-white;
    background-color: $palette-bgcolor;
}

.layer {
    position: fixed;
    left: 0;
    height: 100vh;
    width: 100%;
    background-color: $palette-bgcolor;
    height: 100%;
}

.plane {
    height: 100vh;
    position: absolute;
    z-index: 2;
    left: -50vh;
    height: 100%;
}

.texts {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    h1, .content, p {    
        font-family: "Roboto", sans-serif;
        font-size: clamp(26px, 3.33vw, 64px);
        font-weight: 700;
        letter-spacing: 0.05em;
        text-align: center;
        line-height: 0.7;
    }
}

.bg {
    background-size: cover;
    background-attachment: fixed;
}

.bg-1 {
    background-image: url('/images/bg1.webp');
    height: 240vh;
}

.bg-2 {
    background-image: url('/images/bg2.webp');
    height: 130vh;
}

.welcome-block {
    height: 50vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
}

.welcome-text {
    font-size: clamp(20px, 1.875vw, 36px);
    font-weight: 200;
    letter-spacing: 0.25em;
    line-height: 2.5em;
    color: $palette-white;
    text-transform: uppercase;
}

.transparent-text {
    font-size: clamp(26px, 3.33vw, 64px);
    font-weight: 900;
    letter-spacing: 0;
    background: url('../images/bg1.webp');
    background-size: cover;
    background-attachment: fixed;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}

.accent {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: clamp(48px, 6.25vw, 120px);
    color: transparent;
}
 
.accent-stroke {
    -webkit-text-stroke: 2px $palette-accent;
}

.accent-wave {
    color: $palette-accent;
    animation: wave 4s ease-in-out infinite;
}

.content {
    position: relative;
}

@keyframes wave {
    0%, 100% {
        clip-path: polygon(0% 39%, 9% 41%, 18% 45%, 24% 50%, 31% 55%, 39% 60%, 46% 62%, 53% 62%, 62% 59%, 68% 54%, 76% 50%, 83% 49%, 90% 50%, 97% 52%, 100% 54%, 100% 100%, 0% 100%)
    } 
    50% {
        clip-path: polygon(0 49%, 5% 53%, 11% 57%, 16% 59%, 28% 64%, 38% 57%, 41% 58%, 48% 56%, 54% 58%, 64% 62%, 71% 66%, 79% 68%, 86% 66%, 92% 64%, 100% 62%, 100% 100%, 0% 100%)
    }
}


@media (max-width: 1200px) {
    .plane {
        left: -60vh;
    }
}


@media (max-width: 860px) {
    .texts {
        top: 25%;
        h1, .content, p {
            line-height: 1;
        }
    }
    .plane {
        left: -60vh;
        display: block;
        width: auto;
        height: auto;
        max-width: 100%;
        max-height: 100%;
    }
}

@media (max-width: 768px) {
    .layer {
        height: 100vh;
        height: 100dvh;
    }

    .plane {
        height: 100vh;
        height: 100dvh;
    }
}
</style>