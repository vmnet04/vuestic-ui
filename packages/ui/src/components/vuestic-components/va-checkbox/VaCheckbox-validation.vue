<template>
  <VbCard title="va-input validation">
    <VaCheckbox
      v-model="value"
      label="Name input"
    />
    <VaCheckbox
      v-model="value"
      label="Name"
      :rules="[v => !!v || 'Value should be true']"
    />
  </VbCard>
</template>

<script lang="ts">

import VaCheckbox from './VaCheckbox.vue'
import { Component, Vue } from 'vue-property-decorator'

@Component({
  components: { VaCheckbox },
})
export default class VaCheckboxValidation extends Vue {
  data () {
    return {
      value: false,
    }
  }
}
</script>
