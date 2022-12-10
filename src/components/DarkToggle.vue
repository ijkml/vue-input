<script setup lang="ts">
import { useDark, usePreferredDark, useToggle } from '@vueuse/core';
import { onMounted, ref, watch } from 'vue';

const isDark = useDark();
const toggleDark = useToggle(isDark);

const icon = ref<0 | 1 | 2>(0);

function renderIcon(dark: boolean) {
  icon.value = dark ? 1 : 2;
}

onMounted(() => {
  renderIcon(isDark.value);
});

const prefersDark = usePreferredDark();

watch(prefersDark, (pref) => {
  isDark.value = pref;
});

watch(isDark, () => {
  renderIcon(isDark.value);
});
</script>

<template>
  <button title="Change theme" class="!outline-none" tabindex="0" @click="toggleDark()">
    <Transition name="fade" mode="out-in">
      <span v-if="icon === 1">
        <svg viewBox="0 0 32 32">
          <path
            fill="currentColor"
            d="M16 12.005a4 4 0 1 1-4 4a4.005 4.005 0 0 1 4-4m0-2a6 6 0 1 0 6 6a6 6 0 0 0-6-6ZM5.394 6.813L6.81 5.399l3.505 3.506L8.9 10.319zM2 15.005h5v2H2zm3.394 10.193L8.9 21.692l1.414 1.414l-3.505 3.506zM15 25.005h2v5h-2zm6.687-1.9l1.414-1.414l3.506 3.506l-1.414 1.414zm3.313-8.1h5v2h-5zm-3.313-6.101l3.506-3.506l1.414 1.414l-3.506 3.506zM15 2.005h2v5h-2z"
          />
        </svg>
      </span>
      <span v-else-if="icon === 2">
        <svg viewBox="0 0 32 32">
          <path
            fill="currentColor"
            d="M13.502 5.414a15.075 15.075 0 0 0 11.594 18.194a11.113 11.113 0 0 1-7.975 3.39c-.138 0-.278.005-.418 0a11.094 11.094 0 0 1-3.2-21.584M14.98 3a1.002 1.002 0 0 0-.175.016a13.096 13.096 0 0 0 1.825 25.981c.164.006.328 0 .49 0a13.072 13.072 0 0 0 10.703-5.555a1.01 1.01 0 0 0-.783-1.565A13.08 13.08 0 0 1 15.89 4.38A1.015 1.015 0 0 0 14.98 3Z"
          />
        </svg>
      </span>
      <span v-else>
        <svg viewBox="0 0 32 32">
          <path
            fill="currentColor"
            d="M27.562 26L17.17 8.928l2.366-3.888L17.828 4L16 7.005L14.17 4l-1.708 1.04l2.366 3.888L4.438 26H2v2h28v-2ZM16 10.85L25.22 26H17v-8h-2v8H6.78Z"
          />
        </svg>
      </span>
    </Transition>
  </button>
</template>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 200ms ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

button {
  @apply py-2 px-2.5 bg-zinc-3 text-zinc-9 inline-flex place-items-center
    rounded-md transition duration-300 dark:(bg-zinc-8 text-white);

  >span {
    @apply h-5 w-5;

    >svg {
      @apply h-5 w-5;
    }
  }

  &:focus,
  &:focus-visible {
    @apply outline-none;
  }

  &:hover,
  &:focus-visible {
    @apply bg-zinc-4 dark:(bg-zinc-7);
  }
}
</style>
