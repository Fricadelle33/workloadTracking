<template>
  <div>
    <h3>Hello, world !</h3>
    <div class="q-pa-md q-gutter-sm">
      <q-banner rounded class="bg-indigo-8 text-white">
        <label>What would you like to do, Stranger ?<br/>
          <input type="text" v-model="strangerDesire" />
        </label>

        <template v-slot:action>
          <q-btn color="black" :loading="isSwordLoading" :label=swordLabel @click="simulateProgress()">
            <q-tooltip content-class="bg-accent">Choose wisely, for Odin will not forgive.</q-tooltip>
          </q-btn>
          <q-btn v-if="godModeToggle === 'On'" color="black" :label=torchLabel :ripple="{ color: 'yellow' }" @click="fulfillDreams()"/>
          <q-btn v-else v-show="isLightAvailable" color="green" :label=torchLabel :ripple="{ color: 'yellow' }" @click="fulfillDreams()"/>
        </template>
      </q-banner>
      <q-banner rounded class="text-white" v-if="isLightOn" :class="cls">
        {{ strangerDesire }} has been fulfilled.
      </q-banner>
      <q-toggle
        :label="`God mode: ${godModeToggle}`"
        v-model="godModeToggle"
        false-value="Off"
        true-value="On"
      /><br/>
      <q-btn
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
  name: 'AventureDontVousEtesLeHeros',
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
      strangerDesire: '',
      cls: 'bg-indigo-8'
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
        this.cls = 'bg-red-8'
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

<style lang="scss" scoped>
.successClass {
  background-color: var(bg);
  color: var(primary);
}

.errorClass {
  background-color: var(bg);
  color: red;
}
</style>
