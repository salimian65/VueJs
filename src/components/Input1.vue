<template>
  <div>
    <input
      type="number"
      :value="value"
      @input="onInput"
      @blur="onBlur"
      :class="{ negative: isNegative }"
      v-bind="$attrs"
    />
  </div>
</template>

<script>
export default {
  name: "Input1",
  inheritAttrs: false,
  props: ["value"],
  computed: {
    isNegative() {
      return this.value < 0;
    }
  },
  methods: {
    onInput(e) {
      // You can conditionally do this after validation
      this.$emit("input", e.target.value);
    },
    onBlur() {
      if (this.isNegative) {
        this.$emit("input", 0);
      }
    }
  }
};
</script>