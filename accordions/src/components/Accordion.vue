<template>
    <div class="accordion-container">
        <div class="accordion" v-for="(item, index) in items" :key="index">
            <div class="accordion-header" @click="toggleAccordion(index)">
                {{ item.title }}
                <span class="arrow-icon">{{ item.open ? "▼" : "►" }}</span>
            </div>

            <div class="accordion-content" v-show="item.open">
                {{ item.content }}
            </div>
        </div>
    </div>
</template>

<script setup>

import { ref } from 'vue';

const items = ref([
    {
        title: 'What is HTML?',
        content: 'HTML (HyperText Markup Language) is the standard markup language used to create and structure content on the web.',
        open: false,
    },
    {
        title: 'What is CSS?',
        content: 'CSS (Cascading Style Sheets) is used to style and layout HTML elements, controlling colors, fonts, spacing, and positioning.',
        open: false,
    },
    {
        title: 'What is JavaScript?',
        content: 'JavaScript is a programming language that allows you to make web pages interactive, handling dynamic content, events, and logic.',
        open: false,
    },
    {
        title: 'What is the difference between HTML and CSS?',
        content: 'HTML structures content on the page, while CSS is used to style and visually present that content.',
        open: false,
    },
    {
        title: 'What are HTML tags?',
        content: 'HTML tags are the building blocks of HTML. They define elements such as headings, paragraphs, links, images, and more.',
        open: false,
    },
    {
        title: 'What is the DOM?',
        content: 'The DOM (Document Object Model) is a representation of the web page that JavaScript can interact with to manipulate content and structure.',
        open: false,
    },
    {
        title: 'What is a CSS selector?',
        content: 'A CSS selector targets HTML elements to apply specific styles. Examples include class selectors, ID selectors, and element selectors.',
        open: false,
    },
    {
        title: 'What are JavaScript functions?',
        content: 'Functions are reusable blocks of code in JavaScript that perform a specific task when called.',
        open: false,
    },
    {
        title: 'What is responsive design?',
        content: 'Responsive design ensures a website looks and functions well on devices of all sizes, using flexible layouts and media queries.',
        open: false,
    },
    {
        title: 'What is the difference between inline, internal, and external CSS?',
        content: 'Inline CSS is applied directly on an HTML element, internal CSS is defined in a <style> tag in the HTML file, and external CSS is in a separate .css file linked to the HTML.',
        open: false,
    },
]);

const toggleAccordion = (index) => {
    items.value = items.value.map((item, i) => {
        if (i === index) {
            item.open = !item.open;
        }
        return item;
    });
};

</script>

<style scoped>
.accordion-container {
  max-width: 600px;
  margin: 50px auto;
}

.accordion {
  border: 1px solid #ddd;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 10px;
}

.accordion-header {
  background-color: #3498db;
  color: #fff;
  padding: 15px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.arrow-icon {
  font-size: 20px;
}

.accordion-content {
  padding: 15px;
  display: none;
  border-top: 1px solid #ddd;
  background-color: #f9f9f9;
  color: #333;
}

.accordion-content[style] {
  display: block;
}
</style>