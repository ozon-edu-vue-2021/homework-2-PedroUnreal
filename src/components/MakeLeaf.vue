<template>
  <div>
    <p>{{ space }}+{{ leafNames }}</p>
  </div>
</template>

<script>
export default {
  name: "MakeLeaf",
  props: {
    counter: {
      type: Number,
    },
    leafName: {
      type: String,
    }
  },
  computed: {
    space: "__".repeat(this.counter),
  },
};

console.log(this.leafNames);
