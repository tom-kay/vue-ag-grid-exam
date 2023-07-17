<template>
  <div>
    <button @click="alertClick('￡')">Push</button>
    <span>{{ value }}</span>
  </div>
</template>
<script>
export default {
  setup(props) {
    // eslint-disable-next-line vue/no-setup-props-destructure
    let { value } = props.params;
    // eslint-disable-next-line vue/no-setup-props-destructure
    let { btnText } = props.params;
    function alertClick(s) {
      alert(s + s + s + s + " from " + value);
    }
    return { value, alertClick, btnText };
  },
};
</script>
<style lang="scss"></style>
