<template>
  <div>
    <h3>Hello, world !</h3>
    <div class="q-pa-md q-gutter-sm">
      <q-banner rounded class="bg-indigo-8 text-white">

        What would you like to do, Stranger ?<br/>
        <input type="text" v-model="strangerDesire" />

        <template v-slot:action>
          <q-btn color="black" :loading="isSwordLoading" :label=swordLabel @click="simulateProgress()">
            <q-tooltip content-class="bg-accent">Choose wisely, for Odin will not forgive.</q-tooltip>
          </q-btn>
          <q-btn v-if="godModeToggle === 'On'" color="black" :label=torchLabel :ripple="{ color: 'yellow' }" @click="fulfillDreams()"/>
          <q-btn v-else v-show="isLightAvailable" color="green" :label=torchLabel :ripple="{ color: 'yellow' }" @click="fulfillDreams()"/>
        </template>
      </q-banner>
      <div v-if="isLightOn"><h6>{{ strangerDesire }} has been fulfilled.</h6></div>
      <q-toggle
        :label="`God mode: ${godModeToggle}`"
        v-model="godModeToggle"
        false-value="Off"
        true-value="On"
      /><br/>
      <q-btn
        key="btn_size_round_md"
        round
        color="primary"
        size="md"
        icon="highlight_off"
        @click="reset()"
      />
    </div></div>
</template>

<script>
export default {
  data () {
    return {
      swordOn: 'Unsheathe !',
      swordOff: 'Unsheathed.',
      swordLabel: this.swordOn,
      torchLabel: 'Light the way',
      godModeToggle: 'Off',
      isLightAvailable: false,
      isSwordLoading: false,
      isLightOn: false,
      strangerDesire: ''
    }
  },
  created () {
    console.log('Mon premier log :)')
    this.handleCreated()
  },
  methods: {
    // Load X into Y
    // ------------------------------------
    simulateProgress: function () {
      this.isSwordLoading = true
      setTimeout(this.changeButtonState, 1500)
    },
    // Sheathe the sword and draw the light
    // ------------------------------------
    changeButtonState: function () {
      this.isSwordLoading = false
      this.swordLabel = this.swordOff
      this.isLightAvailable = true
    },
    // Handlers
    // --------
    handleCreated: function () {
      this.swordLabel = this.swordOn
    },
    fulfillDreams: function () {
      if (this.strangerDesire === '') {
        this.strangerDesire = 'Nothing'
      }
      this.isLightOn = true
    },
    // Useful functions
    // ----------------
    reset: function () {
      Object.assign(this.$data, this.$options.data.call(this))
    }
  }
}
</script>

<style scoped>

</style>
