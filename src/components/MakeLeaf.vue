<template>
  <div class="build-tree">
    <div :style="dash" v-on:click="toggleChildren" :class="type">
      <span
        v-on:click="toggleBackground"
        class="item"
        v-bind:class="showBackground ? activeBg : ''"
        v-on:keydown="keydown"
        tabindex="0"
        ref="elem"
      >
        <!-- v-on:focus="toggleChildren"  -->
        <span v-html="emoji[type]"> </span>
        <span>
          {{ name }} {{depth}}
        </span>
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
  mounted: function () {
    window.addEventListener(
      "keydown",
      function (e) {
        if (
          ["Space", "ArrowUp", "ArrowDown", "ArrowLeft", "ArrowRight"].indexOf(
            e.code
          ) > -1
        ) {
          e.preventDefault();
        }
      },
      false
    );
  },
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
      activeFile: "activeFile",
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
    keydown(event) {
      if (event.code == "ArrowRight") {
        event.preventDefault();
        //event.target.focus();
        this.showChildren = true;
        // console.log(event.target);
        // //this.$ref.elem.focus();
        //  this.$nextTick(() => {
        // this.$refs.elem.focus();})
      }

      if (event.code == "ArrowDown") {
        event.preventDefault();
        this.$children[0].$refs.elem.focus()
        //this.$refs.elem.focus();
      }
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

.item:focus {
  border: 5px solid red;
}

.activebg {
  background-color: lightcyan;
}

.activeFile {
  background-color: blueviolet;
  border: crimson solid 2px;
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
