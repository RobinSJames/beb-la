<template>
  <div>
    <b-nav tabs fill>
      <b-nav-item disabled>Another Link</b-nav-item>
      <b-nav-item disabled>Counter: {{ numCorrect }}/{{ numTotal }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ["numCorrect", "numTotal"]
};
</script>
