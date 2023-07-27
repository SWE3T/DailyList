<template>
  <h1>{{ greating }}, {{ userName }}</h1>
  <div class="quote-wrapper">
    "{{quote}}"
    <br>
    -{{author}}
  </div>
</template>

<script>
export default {
  name: "IntroductionText",
  props: ["userName"],
  data() {
    return {
      quote: "",
      author: "", 
    };
  },
  computed: {
    greating() {
      return (Date.now() < 12 ? "Good morning" : Date.now() < 18 ? "Good afternoon" : "Good night")
    },
  },
  async mounted() {
    try {
      const url = "https://type.fit/api/quotes";
      const response = await fetch(url);

      if (!response.ok) throw new Error('Request failed');
      
      const data = await response.json();
      
      const randomIndex = Math.floor(Math.random() * (data.length - 1)) + 1;
      this.quote = data[randomIndex].text;
      this.author = data[randomIndex].author.replace(', type.fit', '') ?? 'Unknown';
    } catch (error) {
      return 'Error';
    }
  }
};
</script>

<style scoped>
  .quote-wrapper {
    max-width: 40%;
    margin: 0 auto;
    font-size: 1.5rem;
  }
</style>

