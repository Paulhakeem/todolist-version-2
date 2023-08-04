<script setup>
import { ref, watch, onMounted } from 'vue';
import InputModal from '../components/InputModal.vue';
import MenuModal from '../components/MenuModal.vue';

const modalActive = ref(null)
const menuModal = ref(null)

const newItem = ref('')
const items = ref([])

const taggleModal = () => {
  modalActive.value = !modalActive.value
}

const openMenu = () => {
  menuModal.value = !menuModal.value
}

const addItem = () => {
  items.value.push({id: items.value.length + 1, label: newItem.value, complete: false})
  newItem.value = ''
}

const removeItems = (index) => {
  items.value.splice(index, 1)
}




watch(items, newItem => {
  localStorage.setItem('items', JSON.stringify(newItem))
}, {deep: true})

watch(items, newItem => {
  localStorage.setItem('items', newItem)
})


//onMounted(() => {
  //newItem.value = localStorage.getItem('newItem') || ''
  //items.value = JSON.parse(localStorage.getItem('items')) || []
//})
</script>

<template>
 <div class="home max-w-md justify-center items-center rounded-lg shadow-lg g-[#f1f2f5] m-auto pt-12">
<MenuModal 
 :menuModal="menuModal"
 @close-menu="openMenu"
>
  <div class="relative space-x-16 mb-10">
    <div class="text-end pt-2 mr-2">
    </div>
     
      <div class="w-20 h-20 bg-gray-400 rounded-full"></div>
       <div class="pt-2">
        <h3 class="text-3xl font-bold text-white">
          Hakeem Paul
        </h3>
       </div>
      <div class="flex pt-6 space-x-4">
        <font-awesome-icon :icon="['fas', 'bookmark']" class="text-2xl text-white"/>
        <p class="text-white font-light">Create your template</p>
      </div>
      <div class="flex pt-6 space-x-4">
        <font-awesome-icon :icon="['fas', 'box']" class="text-2xl text-white"/>
        <p class="text-white font-light">Categories</p>
      </div>
      <div class="flex pt-6 space-x-4">
        <font-awesome-icon :icon="['fas', 'chart-simple']" class="text-2xl text-white"/>
        <p class="text-white font-light">Analytics</p>
      </div>
      <div class="flex pt-6 space-x-4">
        <font-awesome-icon :icon="['fas', 'gear']" class="text-2xl text-white"/>
        <p class="text-white font-light">Settings</p>
      </div>
      <div class="pt-10">
        <span class="text-gray-400 font-light">Good</span>
        <p class="text-white font-medium">Consistency</p>
      </div>
  </div>
</MenuModal>







  <div class="justify-between flex ml-4 mr-4 p-4">
    <div>
      <font-awesome-icon
       @click="openMenu"
       :icon="['fas', 'bars']" 
       class="text-xl text-gray-400 cursor-pointer"/>
    </div>
    <div class="justify-end">
      <font-awesome-icon :icon="['fas', 'magnifying-glass']" class="text-xl text-gray-400"/>
    </div>
    <div>
      <font-awesome-icon :icon="['far', 'bell']" class="text-xl text-gray-400"/>
    </div>
  </div>
  <div class="p-2 ml-4 space-y-4">
    <h3 class="text-2xl font-bold text-gray-800">Welcome Stranger</h3>
    <p class="uppercase text-gray-400 text-xs">categories</p>
  </div>


  <div class="flex items-center space-x-4 ml-4 p-2">
            <div class="relative border-2 pt-2 border-gray-200 p-4 rounded-md w-48">
                <p>40 tasks</p>
                <p class="text-2xl pb-4">Business</p>
                <div class="overflow-hidden h-2 mb-4 text-xs flex rounded bg-pink-200">
                  <div style="width:30%" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-pink-500"></div>
                </div>
              </div>
              <div class="relative pt-1 border-2 border-gray-200 p-4 rounded-md w-48">
                <p>18tasks</p>
                <p class="text-2xl pb-4">Personal</p>
                <div class="overflow-hidden h-2 mb-4 text-xs flex rounded bg-pink-200">
                  <div style="width:30%" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-pink-500"></div>
                </div>
              </div>
              
  </div>
            <div class="ml-4 p-2 space-y-4">
              <p class="uppercase text-xs text-gray-400">
             today's tasks
            </p>
         <transition-group tag="ul" name="list">
          <div class="flex space-y-3 flex-col">
            <li 
             v-for="({id, label}, index) in items" :key="id" 
              class="list-none flex gap-4 cursor-pointer">
              <font-awesome-icon :icon="['far', 'circle']" class="text-purple-400 text-2xl"/>
              <p class="text-gray-600">{{ label }}</p>
                <div></div>
              <font-awesome-icon @click = "removeItems"
              :icon="['fas', 'trash-can-arrow-up']"
               class="text-red-500 text-2xl"/>
            </li>
            </div>
         </transition-group>
          
           </div>











           <InputModal
           :modalActive="modalActive"
           @close-modal="taggleModal">
           <input v-model="newItem"
           type="text" 
           class="border-none outline-none p-2 text-gray-500 text-xl" 
           placeholder="Enter new task">
           <div class="flex space-x-8">
            <div class="border-2 border-gray-300 rounded-full p-1 w-24 flex gap-2">
              <font-awesome-icon :icon="['fas', 'calendar']" class="text-gray-300 pt-1 ml-2 "/>
              <p class="text-gray-300 text-md font-semibold">Today</p>
            </div>
            <div class="w-8 h-8 border-2 border-gray-300 rounded-full">
              <font-awesome-icon :icon="['fas', 'circle-dot']" class="pt-1 text-blue-600 text-xl ml-1" />
            </div>
           </div>
            <div class="space-x-12 ml-8 pt-4">
              <font-awesome-icon :icon="['fas', 'folder-plus']" class="text-gray-400"/>
              <font-awesome-icon :icon="['fas', 'font-awesome']" class="text-gray-400"/>
              <font-awesome-icon :icon="['fas', 'moon']" class="text-gray-400"/>
            </div>
            <div class="justify-end text-right">
              <button 
              @click="addItem"
               class="bg-blue-600 rounded-full p-2 w-28 text-white">
                New task
              </button>
            </div>
          </InputModal>

   <footer>
    <div class="text-right mr-4 pb-6">
      <font-awesome-icon @click="taggleModal"
      :icon="['fas', 'circle-plus']"
       class="fa-3x text-blue-500 cursor-pointer"/>
    </div>
   </footer>
 </div>
</template>


