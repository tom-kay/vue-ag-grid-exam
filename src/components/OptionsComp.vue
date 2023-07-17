<template lang="">
  <div>
    <button @click="onClick">Pull</button>
    {{ value }}
  </div>
</template>
<script>
export default {
  data() {
    return { value: "" };
  },
  beforeMount() {
    this.value = this.params.value;
  },
  methods: {
    onClick() {
      alert("The Age is" + this.value);
    },
  },
};
</script>
<style lang=""></style>
