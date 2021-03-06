<template>
  <v-popover
    :trigger="trigger"
    :open="open"
    :disabled="disabled"
    :placement="placement"
    :auto-hide="autoHide"
    popover-class="va-popover"
    popover-inner-class="va-popover__inner"
    popover-wrapper-class="va-popover__wrap"
  >
    <slot />
    <div
      slot="popover"
      class="va-popover__content"
      :style="computedPopoverStyle"
    >
      <div
        v-if="icon"
        class="va-popover__icon"
      >
        <va-icon
          :name="icon"
          :color="color"
        />
      </div>
      <div v-if="title || message">
        <div
          v-if="title"
          class="va-popover__title"
        >
          {{ title }}
        </div>
        <div class="va-popover__text">
          {{ message }}
        </div>
      </div>
    </div>
  </v-popover>
</template>

<script>
import { VPopover } from 'v-tooltip'
import VaIcon from '../va-icon/VaIcon'
import {
  getHoverColor,
  getBoxShadowColor,
} from '../../../services/color-functions'

export default {
  name: 'VaPopover',
  components: {
    VPopover,
    VaIcon,
  },
  props: {
    color: {
      type: String,
      default: 'success',
    },
    icon: {
      type: String,
      default: '',
    },
    title: {
      type: String,
      default: '',
    },
    message: {
      type: String,
      default: '',
    },
    trigger: {
      type: String,
      default: 'hover',
    },
    open: {
      type: Boolean,
      default: false,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    placement: {
      type: String,
      default: 'bottom',
    },
    autoHide: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    computedPopoverStyle () {
      return {
        boxShadow: '0px 2px 3px 0 ' + getBoxShadowColor(this.$themes[this.color]),
        backgroundColor: getHoverColor(this.$themes[this.color]),
      }
    },
  },
}
</script>

<style lang="scss">
@import '../../vuestic-sass/resources/resources';

.v-popover {
  display: inline;
}

.va-popover {
  opacity: 1;
  border: none;
  border-radius: 0.5rem;
  background-color: white;

  &__content {
    display: flex;
    align-items: center;
    padding: 0.65rem 1rem;
    border-radius: 0.5rem;
    font-size: 1rem;
  }

  &__icon + div {
    padding-left: 0.75rem;
    width: 100%;
    overflow: hidden;
  }

  &__title {
    font-weight: $font-weight-bold;
    margin-bottom: 0.125rem;
  }

  &__text {
    line-height: 1.5;
  }
}
</style>
