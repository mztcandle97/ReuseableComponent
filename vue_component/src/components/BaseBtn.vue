<script lang="ts" setup>
import { QBtn } from 'quasar';

const props = withDefaults(
  defineProps<{
    label?: string | undefined;
    size?: 'sm' | 'md' | 'lg' | 'xl';
    /**
     * Specifies the type of button used. Defaults to primary.
     */
    type?:
      | 'primary'
      | 'secondary'
      | 'negative'
      | 'add'
      | 'highlight'
      | 'icon'
      | 'warning';
    /**
     * Icon name following Quasar convention; Make sure you have the icon library installed unless you are using 'img:' prefix
     */
    icon?: string | undefined;
    iconright?: string | undefined;

    /**
     * Put component in disabled mode
     */
    disable?: boolean;
    submit?: boolean;
  }>(),
  {
    size: 'sm',
    type: 'primary',
  }
);
</script>

<template>
  <q-btn
    :class="`
        btn-${size}
        ${type}
        ${disable ? 'disable' : ''}
      `"
    unelevated
    no-caps
    :label="label"
    :icon-right="iconright"
    :icon="icon"
    :disable="disable"
    :round="type == 'icon' || type == 'warning' || !!$attrs.round"
    :padding="type == 'icon' ? '0' : type == 'warning' ? '12px' : ''"
    :type="submit ? 'submit' : undefined"
  >
    <template v-if="$slots.default" #default>
      <slot></slot>
    </template>
    <template v-if="$slots.loading" #loading>
      <slot name="loading"></slot>
    </template>
  </q-btn>
</template>

<style lang="scss" scoped>
$sizes: (
    'size': sm,
    'font-size': 16px,
  ),
  (
    'size': md,
    'font-size': 18px,
  ),
  (
    'size': lg,
    'font-size': 22px,
  ),
  (
    'size': xl,
    'font-size': 32px,
  );
.q-btn {
  --base-btn-py-sm: 12px;
  --base-btn-py-md: 16px;
  --base-btn-py-lg: 18px;
  --base-btn-py-xl: 20px;
  --base-btn-px: 20px;
  --base-btn-bd-thickness: 3px;
  &.btn-xl {
    --base-btn-px: 60px;
    --base-btn-bd-thickness: 6px;
  }

  &:not(.q-btn--round) {
    border-radius: 10px;
  }
  &:not(.warning) {
    box-shadow: 0px 0px 5px 0px hsla(0, 0%, 0%, 0.3);
  }
  transition: all 150ms ease;
  color: white;

  // On hover (but not pressed)
  &:hover:not(:active) {
    box-shadow: 0px 0px 16px 0px hsla(0, 0%, 0%, 0.26);
  }

  // On pressed
  &:active {
    transform: scale(0.95);
  }

  &.primary {
    background-color: #f7ba50;

    &:hover:not(:active) {
      background: #f5ab2b;
    }

    &:active {
      background: #f5ab2b;
    }
  }
  &.secondary {
    background-color: white;
    color: #f7ba50;

    &:hover:not(:active) {
      color: #f5ab2b;
    }

    &:active {
      color: #f5ab2b;
      background-color: white;
    }
  }

  // &.negative {
  //   background-color: $negative;
  // }
  &.icon {
    padding: 0;
    background-color: white;
    color: $grey-8;
    border: 3px solid white;
    box-shadow: none;

    &.btn-sm {
      :deep(.q-btn__content) {
        padding: 2px;
        font-size: 1.25em;
      }
    }
    &.btn-md {
      :deep(.q-btn__content) {
        padding: 7px;
        font-size: 1.25em;
      }
    }
    &.btn-lg {
      :deep(.q-btn__content) {
        padding: 10px;
        font-size: 2.25em;
      }
    }

    &:hover {
      box-shadow: 0 0 10px 0 hsla(0, 0%, 0%, 0.14);
      border-color: #f7ba50;
      color: #f5ab2b;
    }

    &:active {
      box-shadow: 0px 0px 6px 0px hsla(0, 0%, 0%, 0.5);
      border-color: #f7ba50;
      color: #f5ab2b;
    }
  }

  &.add {
    color: white;
    border: dashed 3px whitesmoke;
    box-shadow: none !important;
    border-radius: 20px;

    &:hover:not(:active) {
      background-color: #f7ba50;
      border-color: #f5ab2b;
      color: white;
    }

    &:active {
      background-color: #f7ba50;
      border-color: #f5ab2b;
      color: white;
    }
  }
  // &.highlight {
  //   color: black;
  //   background-color: $highlight-1;

  //   &:hover:not(:active) {
  //     color: white;
  //     background: #f5ab2b !important;
  //   }

  //   &:active {
  //     background: #f5ab2b !important;
  //   }
  // }

  // &.warning {
  //   color: $negative;
  //   background-color: transparent;

  //   &:hover {
  //     background-color: $negative-inv;

  //     &:active {
  //       background-color: $negative;
  //       color: $negative-inv;
  //     }
  //   }
  // }

  // &.disable {
  //   background-color: $grey-4 !important;
  //   color: $grey-7 !important;
  //   border-color: $grey-7 !important;
  //   box-shadow: none !important;
  //   opacity: 1 !important;
  //   // because .disable makes things slightly transparent
  // }

  &.secondary {
    border: var(--base-btn-bd-thickness) solid currentColor;
  }

  // Hide the grey overlay that comes with q-btn
  &:not(.warning) :deep(.q-focus-helper) {
    display: none;
  }

  :deep(.q-icon) {
    // to fit font-size + line-height for labels
    font-size: calc(1em + 4px);
  }

  @each $size in $sizes {
    &.btn-#{map-get($size, 'size')} {
      padding: var(--base-btn-py-#{map-get($size, 'size')}) var(--base-btn-px);
      &.secondary {
        padding: calc(
            var(--base-btn-py-#{map-get($size, 'size')}) -
              var(--base-btn-bd-thickness)
          )
          calc(var(--base-btn-px) - var(--base-btn-bd-thickness));
      }
      :deep(.q-btn__content) {
        font-size: map-get($size, 'font-size');
        line-height: calc(1em + 4px);
        font-weight: 600;
      }
    }
  }
}
</style>
