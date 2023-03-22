<template>
    <audio controls>
      <source :src="link" type="audio/mpeg">
    </audio>
</template>
<script>
export default {
  name: "Card",
  props: {
    link: String,

  },
};
</script>