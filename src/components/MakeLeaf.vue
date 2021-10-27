<template>
  <div class="tree-menu">
    <div :style="indent" v-on:click="toggleChildren" v-bind:class="[isDir ? activeClass : '']">
      {{ name }}
    </div>
    <MakeLeaf
      v-if="showChildren"
      v-for="content in contents"
      :contents="content.contents"
      :name="content.name"
      :key="content.name"
      :depth="depth + 1"
      :type="content.type"
    >
    </MakeLeaf>
  </div>
</template>
<script>
export default {
  props: ["name", "contents", "depth", "type"],
  name: "MakeLeaf",
  computed: {
    indent() {
      return { transform: `translate(${this.depth * 50}px)` };
    },
    },
  data() {
    return { showChildren: false, isDir: this.type === "directory" }    
  },
  methods: {
    toggleChildren() {
      this.showChildren = !this.showChildren;
    },
  },
};
</script>
