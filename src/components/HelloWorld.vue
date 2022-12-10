<script setup lang="ts">
import TheInput from '@/components/TheInput.vue';
</script>

<template>
  <div class="greetings">
    <h1 class="green">
      Vue-Input
    </h1>
    <p class="mb-3">
      One <kbd>&lt;input&gt;</kbd> to rule them all!
    </p>
    <div class="sandbox">
      <form>
        <TheInput class="the-input" />
      </form>
    </div>
  </div>
</template>

<style scoped lang="scss">
h1 {
  font-weight: 500;
  font-size: 2rem;
  top: -10px;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}

.sandbox {
  @apply my-5 bg-white dark:bg-black flex w-full p-5;
}

form {
  @apply w-full;
}

.the-input {
  // @apply w-full;
}
</style>
