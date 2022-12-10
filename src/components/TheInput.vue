<script setup lang="ts">
import { ref } from 'vue';

// interface Props {
//   label?: string
// }

// const props = withDefaults(defineProps<Props>(), {
//   label: undefined,
// });

// ------ possible props -----------//

const inputLabel = 'Form Input Label';
const inputPlaceholder = 'Form Input Placeholder';
const inputBg = '';
const inputColor = '';
const inputActiveColor = 'hotpink';

// ------ possible props -----------//

const elem = ref<HTMLInputElement | null>(null);

const isFocused = ref(false);

const inputValue = ref('');

function setFocus(on: boolean) {
  if (on || inputValue.value) {
    setTimeout(() => {
      isFocused.value = true;
    });
    return;
  }

  isFocused.value = false;
}
</script>

<template>
  <div class="input-box" :class="{ focus: isFocused }">
    <label class="input-label">{{ inputLabel }}</label>
    <input
      v-model.trim="inputValue"
      type="text"
      class="input-1"
      :placeholder="inputPlaceholder"
      @focus="setFocus(true)"
      @blur="setFocus(false)"
    >
  </div>
</template>

<style scoped lang="scss">
.input-box {
  @apply relative z-auto mx-10px;

  // default bg-color
  --default-bg-color: hsl(0, 0%, 100%);
  // default text color
  --default-tx-color: hsl(210, 29%, 24%);

  .dark & {
    // default dark-mode bg-color
    --default-bg-color: hsl(0, 0%, 7%);
    // default dark-mode text color
    --default-tx-color: hsla(0, 0%, 92%, 0.7);
  }

  --prop-bg-color: v-bind(inputBg); // bg color
  --prop-tx-color: v-bind(inputColor); // text color
  --prop-active-color: v-bind(inputActiveColor); // active color

  // --- exposed with defaults
  --input-bg-color: var(--prop-bg-color, var(--default-bg-color));
  --input-text-color: var(--prop-tx-color, var(--default-tx-color));
  --input-active-color: var(--prop-active-color, currentColor);
}

.input-label {
  @apply absolute text-16px font-normal overflow-hidden text-ellipsis
    whitespace-nowrap pointer-events-none select-none z-1 left-2
      py-0 px-2 top-1/2;

  contain: layout paint;
  max-width: calc(100% - 16px);
  transform: translateY(-50%);
  transition: 250ms;
  color: var(--input-text-color);
}

.input-1 {
  @apply box-border w-full rounded px-4 py-13px border-none
    outline outline-1 outline-zinc-4 dark:(outline-zinc-7);

  transition: 250ms;
  letter-spacing: 0.009375em;
  background: var(--input-bg-color);
  color: var(--input-text-color);

  &:focus {
    outline: solid 2px;
    outline-color: var(--input-active-color);
  }

  &::placeholder,
  &::-webkit-input-placeholder {
    @apply transition-all duration-180 delay-80 color-inherit opacity-75;
  }

  .input-box:not(.focus) &,
  &:not(:focus) {
    &::placeholder {
      @apply opacity-0;
    }
  }
}

.input-box.focus {
  .input-label {
    color: var(--input-active-color);
    top: -8px;
    background: var(--input-bg-color);
    font-size: 11px;
    transform: translateY(0%);

    transition: 250ms;
  }
}

// forget below

.input-box.error {
  .input-label {
    // color: $error-color; // #f44336
    top: -8px;
    // background: $default-background;
    font-size: 11px;
    transition: 250ms;
  }

  .input-1 {
    // border: 2px solid $error-color; // #f44336
  }
}
</style>