<template>
  <div id="app">
    <MakeLeaf 
      :name="this.json.name" 
      :contents="this.json.contents"
      :depth="0"
      :type="this.json.type">
    </MakeLeaf>
  </div>
</template>

<script>
  import MakeLeaf from "@/components/MakeLeaf.vue";
  import tree from '../public/static/node_modules';

  export default {
    name: "App",
    components: {
      MakeLeaf,
    },
    data() {
      return {
        json: tree
      };
    },
  };
</script>

<style>
  body {
    font-family: "Open Sans", sans-serif;
    font-size: 18px;
    font-weight: 300;
    line-height: 1em;
  }

  .container {
    width: 300px;
    margin: 0 auto;
  }
</style>
