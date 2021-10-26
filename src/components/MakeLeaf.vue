<template>
  <div>
    <p>{{ space + leafName }}</p>
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
      default: ''
    }
  },
  computed: {
    space() { 
      return "__".repeat(this.counter) 
    },
  },
};
</script>
