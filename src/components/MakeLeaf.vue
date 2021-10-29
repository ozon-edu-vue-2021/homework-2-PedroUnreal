<template>
  <div class="build-tree">
    <div 
    :style="dash" 
    v-on:click="toggleChildren"
    :class="type" >
      <span
        v-on:click="toggleBackground"
        class="item"
        v-bind:class="showBackground ? activeBg : ''"
        v-on:keydown="keydown"
        tabindex="0"
        ref="elem"
        autofocus
      >
        <!-- v-on:click="$emit('print-path', path)"  -->
        <span v-html="emoji[type]"> </span>
        <span> {{ name }}/</span>
      </span>
      </div>

      <div v-if="showChildren">
        <MakeLeaf
          v-for="(content, index) in contents"
          :contents="content.contents"
          :name="content.name"
          :key="content.name"
          :depth="depth + 1"
          :type="content.type"
          :index="index"
          :path="path+'/'+name"
          :setPath="setPath"
        >
        </MakeLeaf>
      </div>
    </div>
  <!-- </div> -->
</template>
<script>
export default {
  props: ["name", "contents", "depth", "type", "index", "path", "setPath"],
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
      // this.$parent.$emit('print-path', this.path);
      this.setPath(this.path);
      if (this.type === "directory") return;
      this.showBackground = !this.showBackground;
    },
    keydown(event) {
      if (event.code === ('ArrowRight' )) {
        event.preventDefault();
        this.showChildren = true;
        this.setPath(this.path);
        this.$nextTick(() => {
          if (this.$children[0]) {
            this.$children[0].$refs.elem.focus();
          }
        });
      }

      if (event.code === ('Enter')) {
        event.preventDefault();
        this.setPath(this.path);
        this.showChildren = true;
        this.$nextTick(() => {
          if (this.$children[0]) {
            this.$children[0].$refs.elem.focus();
          }
        });
      }

      if (event.code == "ArrowLeft") {
        event.preventDefault();
        this.setPath(this.path);
        this.showChildren = false;
        this.$parent.showChildren = false;
        if (this.$parent.$refs.elem) {
          this.$parent.$refs.elem.focus();
        }
      }

      if (event.code == "ArrowDown") {
        event.preventDefault();
        this.setPath(this.path);
        if (this.$parent.$children[this.index + 1]) {
          this.$parent.$children[this.index + 1].$refs.elem.focus();
        }
      }

      if (event.code == "ArrowUp") {
        event.preventDefault();
        this.setPath(this.path);
        if (this.$parent.$children[this.index - 1]) {
          this.$parent.$children[this.index - 1].$refs.elem.focus();
        }
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
