<template>
  <div class="flex items-center min-h-screen justify-center">
    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
            @click="toggleDrawer"
    >
      Toggle Drawer
    </button>

    <side-drawer v-model="openDrawer" title="My title">
      <div class="border border-dashed border-gray-300 w-full min-h-screen p-4">
        Side drawer content
      </div>
    </side-drawer>
  </div>
</template>

<script>
import SideDrawer from "@/components/SideDrawer";

export default {
  name: 'App',
  components: {
    SideDrawer
  },
  data() {
    return {
      openDrawer: false
    }
  },
  methods: {
    toggleDrawer() {
      this.openDrawer = !this.openDrawer
    }
  }
}
</script>

<style>
</style>
