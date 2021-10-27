<template>
  <div class="tree-menu">
    <div :style="indent" v-on:click="toggleChildren" :class="type">
      <span v-html="emoji[type]"> </span> 
      <span> {{ name }} </span>

      <div v-if="showChildren">
        <MakeLeaf
          v-for="content in contents"
          :contents="content.contents"
          :name="content.name"
          :key="content.name"
          :depth="depth + 1"
          :type="content.type"
        >
        </MakeLeaf>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["name", "contents", "depth", "type"],
  name: "MakeLeaf",
  computed: {
    indent() {
      return { transform: `translate(${this.depth * 10}px)` };
    },
  },
  data() {
    return { 
      showChildren: false,
      emoji: {
        directory: "&#128193;",
        file: "&#128196;",
        link: "	&#128279;"
      } 
      
    }    
  },
  methods: {
    toggleChildren(e) {
      e.stopPropagation();
      this.showChildren = !this.showChildren;
    },
  },
};
</script>

 <style scoped>

 .tree-menu {
   margin: 5px  0
 }

 .directory {
   color:grey
 }

 .file {
   color:black
 }

 .link {
   color:blue
 }
 
 </style>
