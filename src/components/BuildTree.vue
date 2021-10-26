<template>
  <div class="tree">
    <p>{{ tree }}</p>
    <button v-on:click="BuildTree">Построить дерево</button>
  </div>
</template>

<script>
import MakeLeaf from "@/components/MakeLeaf.vue";
export default {
  name: "BuildTree",
//   components: {
//     MakeLeaf
//   },
  props: {
    msg: String,
  },
  data() {
    return {
      tree: "Дерево",
      counter: 0,
      json: {
        type: "directory",
        name: "code-frame",
        contents: [
          {
            type: "file",
            name: "LICENSE",
          },
          {
            type: "file",
            name: "README.md",
          },
          {
            type: "directory",
            name: "lib",
            contents: [
              {
                type: "file",
                name: "index.js",
              },
              {
                type: "directory",
                name: "dir",
                contents: [
                  {
                    type: "file",
                    name: "index3.js",
                  },
                ],
              },
              {
                type: "file",
                name: "index2.js",
              },
            ],
          },
          {
            type: "file",
            name: "package.json",
          },
        ],
      },
    };
  },
  methods: {
    BuildTree() {
      let json = this.json;
      function printFile(obj) {
        //console.log(obj.name);
        <MakeLeaf v-bind:counter="counter" v-bind:leafName="obj.name">
          {" "}
        </MakeLeaf>; //(a.repeat(counter) + obj.name, counter)
        if (!Array.isArray(obj.contents /*|| obj.contents.length < 1*/)) {
          return;
        }

        //this.counter++;
        obj.contents.forEach((child) => printFile(child));
        //this.counter--;
      }

      printFile(json);
    },
  },
};

// json = JSON.stringify(json);
// json = JSON.parse(json)
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
