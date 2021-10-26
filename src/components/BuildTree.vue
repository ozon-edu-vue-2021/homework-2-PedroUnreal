<template>
  <div class="tree">
    <button v-on:click="BuildTree">Построить дерево</button>
    <!-- <MakeLeaf v-bind:counter="counter" v-bind:leafName="obj.name"/> -->
    <ul>
      <li v-for="(item, index) in tree" v-bind:key="index">
        <MakeLeaf v-bind:leafName="item.name" v-bind:counter="item.counter"></MakeLeaf>
      </li>
    </ul> 
  </div>
</template>

<script>
import MakeLeaf from "@/components/MakeLeaf.vue";

export default {
  name: "BuildTree",
  components: {
    MakeLeaf,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      tree: [],
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
      const self = this;

      function printFile(obj) {
        // <MakeLeaf v-bind:counter="counter" v-bind:leafName="obj.name">
        //   {" "}
        // </MakeLeaf>;
        self.tree.push({ 
          name: obj.name, 
          counter: self.counter 
        });

        if (!Array.isArray(obj.contents) || obj.contents.length < 1) {
          return;
        }

        console.log(self.tree, 'tree 2');

        self.counter++;

        obj.contents.forEach((child) => printFile(child));

        self.counter--;
      }

      printFile(this.json);
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
  display: block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
