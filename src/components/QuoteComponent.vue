<template>
  <div>
    <ul>
        <li class="quote">"{{ quote.quote }}"</li>
        <li class="source"> - {{ quote.source }}</li>
        <li class="context">{{ quote.context }}</li>
        <li>{{ quote.theme }}</li>

    </ul>
  </div> 
</template>

<script>
  export default {
    name: "QuoteComponent",
    props: ["quote"]
  };
</script>

<style>
  ul {
    list-style-type: none;
    
  }

  .context {
    font-style: normal;
    font-weight: 500;
    text-transform: uppercase;
  }

  .quote {
    display: block;
    font-family: Georgia, serif;
    font-size: 18px;
    font-style: italic;
    color: darkgray;
  }
</style>
