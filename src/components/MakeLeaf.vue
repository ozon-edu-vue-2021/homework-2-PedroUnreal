<template>
  <div class="build-tree">
    <div :style="dash" v-on:click="toggleChildren" :class="type">
      <span
        v-on:click="toggleBackground"
        class="item"
        v-bind:class="showBackground ? activeBg : ''"
      >
        <span v-html="emoji[type]"> </span>
        <span> {{ name }} </span>
      </span>

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
    dash() {
      return { transform: `translate(${this.depth * 10}px)` };
    },
  },
  data() {
    return {
      showChildren: false,
      showBackground: false,
      activeBg: "activebg",
      emoji: {
        directory: "&#128193;",
        file: "&#128196;",
        link: "&#128279;",
      },
    };
  },
  methods: {
    toggleChildren(e) {
      e.stopPropagation();
      this.showChildren = !this.showChildren;
    },
    toggleBackground() {
      if (this.type === "directory") return;
      this.showBackground = !this.showBackground;
    },
  },
};
</script>

<style scoped>
.build-tree {
  margin: 5px 0;
  user-select: none;
}

.item {
  cursor: pointer;
}

.activebg {
  background-color: lightcyan;
}

.directory {
  color: grey;
}

.file {
  color: black;
}

.link {
  color: blue;
}
</style>
