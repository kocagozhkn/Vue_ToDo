<template>
  <li :class="{decorated:dana}" v-on:click="emitli">
    {{motor}}
    <button v-on:click="emitbtn">X</button>
  </li>
</template>

<script>
export default {
  name: "HelloWorld",
  props: { motor: "", dana: false },
  data: function() {
    return {};
  },
  methods: {
    emitbtn: function() {
      this.$emit(`btnemitter`, this.motor);
    },
    emitli: function() {
      this.$emit(`liemitter`, 1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.decorated {
  text-decoration: line-through;
}
</style>
