<script>
export default {
  name: "BaseInput",
  props: ["value"],
  inheritAttrs: false,
  data() {
    return {
      label: "dddddd"
    };
  },

  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: event => {
          this.$emit("input", event.target.value);
        }
      };
    }
  }
};
</script>

<template>
  <div>
    <!--  @input="$emit('input',$event.target.value)"-->
    <label>{{label}}</label>
    <input :value="value" v-on="listeners" />
  </div>
</template>
<style scoped>
input {
  background: red;
  width: 200px;
  height: 50px;
}
</style>