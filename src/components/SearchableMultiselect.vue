<template>
  <QChipsInput
    v-model="chips"
    :color="color"
    :chips-bg-color="chipsBgColor"
    @input="inputted"
  >
    <QAutocomplete
      :debounce="debounce"
      :min-characters="minCharacters"
      :max-results="maxResults"
      @search="search"
      @show="show"
      @hide="hide"
      @selected="selected"
    />
  </QChipsInput>
</template>

<script>
export default {
  name: 'SearchableMultiselect',
  props: {
    value: {
      type: Array,
      default: Array
    },
    color: {
      type: String,
      default: null
    },
    chipsBgColor: {
      type: String,
      default: null
    },
    debounce: {
      type: Number,
      default: null
    },
    minCharacters: {
      type: Number,
      default: null
    },
    maxResults: {
      type: Number,
      default: null
    }
  },
  data() {
    return {
      chips: [],
      chipsClone: [],
      isAutocompleting: false
    }
  },
  computed: {
    chipVals: {
      get() {
        return this.value
      },
      set(value) {
        this.$emit('input', value)
      }
    }
  },
  methods: {
    search(terms, done) {
      this.$emit('search', terms, done)
    },
    show() {
      this.isAutocompleting = true
    },
    hide() {
      this.isAutocompleting = false
    },
    selected(item) {
      // Append into chipVals & chipsClone.
      if (this.chips.length > this.chipVals.length) {
        this.chipVals.push(item.id)
        this.chipsClone.push(item.value)
      }
    },
    inputted(newVal) {
      if (!this.isAutocompleting) {
        // Prevent adding custom chip.
        if (newVal.length > this.chipVals.length) {
          this.chips.pop()
        }
        // Sync removed chip.
        else if (newVal.length < this.chipVals.length) {
          this.chipsClone.forEach((name, idx) => {
            if (!newVal.includes(name)) {
              this.chipVals.splice(idx, 1)
              this.chipsClone.splice(idx, 1)
            }
          })
        }
      }
    },
    clearChips() {
      this.chips = []
      this.chipsClone = []
      this.chipVals = []
    },
    setChips(items) {
      const [labels, values] = items.reduce(
        (result, item) => {
          result[0].push(item.label)
          result[1].push(item.value)
          return result
        },
        [[], []]
      )

      this.chips = labels
      this.chipsClone = labels
      this.chipVals = values
    }
  }
}
</script>
