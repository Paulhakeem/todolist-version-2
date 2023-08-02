<script setup>
defineEmits(['close-menu'])
defineProps({
    menuModal: {
        type: Boolean,
        default: false,
    }
})
</script>

<template>
<transition name="modal-outer">
<div class="absolute min-h-0 flex-1 z-40 flex overflow-hidden h-screen">
    <transition name="modal-inner">

    <nav v-show="menuModal"
    aria-label="Sidebar" class="narrow-sidebar hidden
    lg:block bg-pink-700 self-start w-72 rounded-lg">
    <div class="text-end pt-2 mr-2">

      <font-awesome-icon @click="$emit('close-menu')"
      :icon="['far', 'circle-xmark']"
      class="text-2xl text-white cursor-pointer" />
    </div>

   <slot/>
    </nav>
    </transition>
   
</div>
</transition>
</template>




<style scoped>
.modal-outer-enter-active,
.modal-outer-leave-active {
    transition: opacity 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);

}

.modal-outer-enter-from,
.modal-outer-leave-to {
    opacity: 1;
}


</style>