<template>
  <div id="app" v-on:print-path="onPathChange">
    <div class="path">{{ globalPath }}</div>
    <div class="wrapper">
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
      globalPath: "",
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
  top: 0;
  width: 100%;
  background-color: white;
  z-index: 10;
  border: solid red 1px;
  padding: 10px 8px;
}

body {
  margin: 0;
  font-family: "Open Sans", sans-serif;
  font-size: 18px;
  font-weight: 300;
  line-height: 1em;
}

.wrapper {
  margin-left: 8px;
}
</style>
