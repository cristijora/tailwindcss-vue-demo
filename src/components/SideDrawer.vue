<template>
  <div v-if="modelValue"
       class="fixed inset-0 overflow-hidden"
  >
    <div class="absolute inset-0 overflow-hidden bg-black bg-opacity-25"
         @click.self="triggerClose"
    >
      <section class="absolute inset-y-0 right-0 pl-10 flex max-w-full">
        <transition enter-from-class="translate-x-full"
                    enter-to-class="translate-x-0"
                    enter-active-class="transform transition ease-in-out duration-300"
                    leave-active-class="transform transition ease-in-out duration-300"
                    leave-from-class="translate-x-0"
                    leave-to-class="translate-x-full"
                    @after-enter="focusOnClose"
                    @after-leave="closeDrawer">
          <div v-if="open"
               class="w-screen max-w-md">
            <div class="h-full bg-white shadow-xl overflow-y-scroll py-6 space-y-6">
              <header class="px-4 flex items-start justify-between">
                <h2 class="text-lg leading-6 font-medium text-gray-800">
                  <slot name="title">
                    {{ title }}
                  </slot>
                </h2>
                <button class="text-gray-500 rounded hover:text-gray-600 focus:shadow-outline focus:outline-none"
                        ref="closeButton"
                        aria-label="Close drawer"
                        @click="triggerClose"
                >
                  <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                          d="M6 18L18 6M6 6l12 12"></path>
                  </svg>
                </button>
              </header>
              <div class="px-4 flex relative">
                <slot>
                </slot>
              </div>
            </div>
          </div>
        </transition>
      </section>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      default: 'My header'
    },
    modelValue: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      open: false
    }
  },
  methods: {
    triggerClose() {
      this.open = false
    },
    closeDrawer() {
      this.$emit('update:modelValue', false)
    },
    focusOnClose() {
      this.$refs.closeButton.focus()
    },
    onKeyDown(evt) {
      if (evt.key === 'Escape') {
        this.triggerClose()
      }
    },
    initEventListeners() {
      window.addEventListener('keydown', this.onKeyDown)
    },
    removeEventListeners() {
      window.removeEventListener('keydown', this.onKeyDown)
    }
  },
  watch: {
    modelValue(value) {
      if (value) {
        this.open = true
      }
    }
  },
  mounted() {
    this.initEventListeners()
  },
  onBeforeUnmount() {
    this.removeEventListeners()
  }
}
</script>
<style>
</style>
