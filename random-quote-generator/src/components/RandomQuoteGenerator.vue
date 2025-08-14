<template>
    <div class="quote-generator">
        <h1 class="app-title">Random Quote Generator</h1>
        <blockquote class="quote-container">
            <p>{{ currentQuote.text }}</p>
            <cite>{{ currentQuote.author }}</cite>
        </blockquote>
        <button class="quote-button" @click="getRandomQuote">Get Random Quote</button>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const quotes = ref([
  { text: "The best way to get started is to quit talking and begin doing.", author: "Walt Disney" },
  { text: "Don’t let yesterday take up too much of today.", author: "Will Rogers" },
  { text: "It’s not whether you get knocked down, it’s whether you get up.", author: "Vince Lombardi" },
  { text: "If you are working on something exciting, it will keep you motivated.", author: "Steve Jobs" },
  { text: "Success is not in what you have, but who you are.", author: "Bo Bennett" },
  { text: "Don’t watch the clock; do what it does. Keep going.", author: "Sam Levenson" },
  { text: "Hard work beats talent when talent doesn’t work hard.", author: "Tim Notke" },
  { text: "It always seems impossible until it’s done.", author: "Nelson Mandela" },
  { text: "Do something today that your future self will thank you for.", author: "Sean Patrick Flanery" },
  { text: "All our dreams can come true, if we have the courage to pursue them.", author: "Walt Disney" },
  { text: "The future belongs to those who believe in the beauty of their dreams.", author: "Eleanor Roosevelt" },
  { text: "If you can dream it, you can do it.", author: "Walt Disney" },
  { text: "If your dreams don’t scare you, they aren’t big enough.", author: "Lowell Lundstrum" },
  { text: "If you can’t dream big, ridiculous dreams, what’s the point in dreaming at all?", author: "Ronda Rousey" },
  { text: "All men of action are dreamers.", author: "James Huneker" },
  { text: "Dreams come in a size too big so that we may grow into them.", author: "Josie Bissett" },
  { text: "There is only one thing that makes a dream impossible to achieve: the fear of failure.", author: "Paulo Coelho" },
  { text: "Logic will get you from A to B. Imagination will take you everywhere.", author: "Albert Einstein" },
  { text: "You can’t put a limit on anything. The more you dream, the farther you get.", author: "Michael Phelps" },
  { text: "Never give up on a dream just because of the time it will take to accomplish it. The time will pass anyway.", author: "Earl Nightingale" },
]);

const currentQuote = ref({text: '', author: ''});

const getRandomQuote = () => {
    const randomIndex = Math.floor(Math.random() * quotes.value.length);
    currentQuote.value = quotes.value[randomIndex];
    
};

onMounted(() => {
    getRandomQuote();
});

</script>

<style scoped>
.quote-generator {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app-title {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.quote-container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-bottom: 20px;
}

p {
  font-size: 18px;
  margin-bottom: 10px;
}

cite {
  font-style: normal;
  color: #777;
}

.quote-button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.quote-button:hover {
  background-color: #2980b9;
}
</style>