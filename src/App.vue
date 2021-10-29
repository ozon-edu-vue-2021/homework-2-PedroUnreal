<template>
  <div id="app" v-on:print-path="onPathChange">
    <span class="path">{{ globalPath }}</span>
    <MakeLeaf
      :name="this.json.name"
      :contents="this.json.contents"
      :depth="0"
      :type="this.json.type"
      :path="''"
      :setPath="onPathChange"
    >
    </MakeLeaf>
  </div>
</template>

<script>
import MakeLeaf from "@/components/MakeLeaf.vue";
import tree from "../public/static/node_modules";

export default {
  name: "App",
  components: {
    MakeLeaf,
  },
  data() {
    return {
      json: tree,
      globalPath: 0,
    };
  },
  methods: {
    onPathChange(newPath) {
      this.globalPath = newPath;
    },
  },
};
</script>

<style>
#app {
  position: relative;
  margin-top: 50px;
}
.path {
position: fixed;
top: 10px;
background-color: white;
z-index: 10;
border: solid red 1px;
padding: 5px;
}  


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
