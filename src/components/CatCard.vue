<template>
  <div class="card bg-base-100 w-72 shadow-sm">
    <img :src="imageUrl" alt="Cat image" class="w-full h-64 object-cover" />
  </div>
</template>

<script>
export default {
  props: {
    imageUrl: {
      type: String,
      required: true,
    },
  },
};
</script>
