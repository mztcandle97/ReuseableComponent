<template>
  <q-dialog v-model="showModal">
    <q-card
      class="q-pa-sm column no-wrap"
      :style="[{ width: width, height: height }, style]"
    >
      <q-card-section class="q-pa-none q-mb-sm">
        <div class="text-lg-body em text-center">
          <slot name="header" />
        </div>
        <q-btn
          v-if="!hideXBtn"
          class="close-btn"
          padding="0"
          dense
          flat
          icon="close"
          @click="onClose"
        />
      </q-card-section>

      <q-card-section class="q-pa-none text-body col">
        <slot name="body" />
      </q-card-section>

      <q-card-actions
        v-if="$slots.buttons"
        class="q-pa-none tw-mt-5"
        :align="buttonAlign"
      >
        <!-- TODO: make all the buttons in here the same -->
        <slot name="buttons" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script lang="ts">
import { computed, defineComponent, PropType, StyleValue } from 'vue';

export default defineComponent({
  props: {
    width: {
      type: String,
      default: '500px',
    },
    height: {
      type: String,
      default: null,
    },
    show: {
      type: Boolean,
      default: true,
    },
    buttonAlign: {
      type: String as PropType<'center' | 'right' | 'left'>,
      default: 'center',
    },
    /**
     * Hides the x button on the top left of the modal. Defaults to false (show).
     */
    hideXBtn: {
      type: Boolean,
    },
    /*
     * Any css stylings which would be passed into the dialog card
     */
    style: {
      type: Object as PropType<StyleValue>,
    },
  },
  setup(props, { emit }) {
    const showModal = computed({
      get: () => props.show,
      set: (val) => emit('update:show', val),
    });

    const onClose = () => {
      showModal.value = false;
      emit('update:modelValue', false);
    };

    return {
      showModal,
      onClose,
    };
  },
});
</script>

<style lang="scss" scoped>
.q-card {
  max-width: 90vw;
  max-height: 90vh;
  border-radius: 20px;
  padding: 30px;
  @media screen and (max-width: 600px) {
    padding: 10px;
  }

  .close-btn {
    position: absolute;
    top: 0;
    right: 0;
  }
}
</style>
