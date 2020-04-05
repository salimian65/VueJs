<template>
  <div>
    <div>
      <textarea :value="value" @input="input" v-on="listeners" :rows="rows" v-bind="attrs"></textarea>
      {{value}}
    </div>
  </div>
</template>

<script>
import autosize from "autosize";
export default {
  name: "Autosize",
  props: ["value"],
  inheritAttrs: false,
  computed: {
    listeners() {
      const { input, ...listeners } = this.$listeners;
      return listeners;
    },
    rows() {
      return this.$attrs.rows || 3;
    },
    attrs() {
      const { rows, ...attrs } = this.$attrs;
      return attrs;
    }
  },
  methods: {
    input(event) {
      this.$emit("input", event.target.value);
    }
  },
  mounted() {
    autosize(this.$el);
  }
};
</script>

<style scoped>
</style>