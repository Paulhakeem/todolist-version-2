<script setup>
defineEmits(["close-modal"])
defineProps({
    modalActive: {
        type: Boolean,
        default: false,
    }
})

</script>

<template>
    <transition name="modal-outer">
        <div v-show="modalActive"
    class="absolute bg-black w-full z-50 bg-opacity-30 h-screen top-0 left-0 flex justify-center px-8">
    <transition name="modal-inner">
        <div v-if="modalActive"
        class="p-4 bg-white self-start mt-32 max-w-md rounded-lg space-y-8">
        <div class="">
            <font-awesome-icon  
            @click="$emit('close-modal')"
            :icon="['far', 'circle-xmark']" class="text-3xl text-gray-500 cursor-pointer"/>
          </div>
    <slot/>
    </div>
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
    opacity: 0;
}

.modal-inner-enter-active {
    transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02) 0.15s;
}

.modal-inner-leave-active {
    transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-inner-enter-from{
    opacity: 0;
    transform: scale(0.8);
}

.modal-inner-leave-to {
    transform: scale(0.8);
}
</style>