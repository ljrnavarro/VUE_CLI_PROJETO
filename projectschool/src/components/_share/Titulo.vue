<template>
  <div>
    <h1>{{ this.texto }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    texto: String
  }
};
</script>

<style lang="scss" scoped></style>
