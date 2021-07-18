<template>
  <div class="bg-gray-100 rounded-sm m-1 pt-3 pb-5 cursor-pointer">
    <h3 class=" flex justify-between px-2">
      {{ task.text }}
      <i class="fas fa-times text-red-500" @click="openModal()"></i>
    </h3>
  </div>
  <TransitionRoot appear :show="isOpen" as="template">
    <Dialog as="div" @close="closeModal">
      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div class="min-h-screen px-10 text-center">
          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0"
            enter-to="opacity-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100"
            leave-to="opacity-0"
          >
            <DialogOverlay />
          </TransitionChild>

          <span class="inline-block h-screen align-middle" aria-hidden="true">
            &#8203;
          </span>

          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0 scale-95"
            enter-to="opacity-100 scale-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100 scale-100"
            leave-to="opacity-0 scale-95"
          >
            <div
              class="inline-block w-full max-w-md p-6 my-8 overflow-hidden text-left align-middle transition-all transform bg-white shadow-xl rounded-2xl"
            >
              <DialogTitle
                as="h3"
                class="text-lg font-medium leading-6 text-gray-900"
              >
                Do you really want to delete?
              </DialogTitle>
              <div class="mt-4">
                <button
                  type="button"
                  class="inline-flex justify-center px-4 py-2 text-sm font-medium text-blue-900 bg-blue-100 border border-transparent rounded-md hover:bg-blue-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 focus-visible:ring-blue-500"
                  @click="onDelete(curId)"
                >
                  Yes
                </button>
                <button
                  type="button"
                  class="inline-flex justify-center px-4 py-2 ml-2 text-sm font-medium text-blue-900 bg-blue-100 border border-transparent rounded-md hover:bg-blue-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 focus-visible:ring-blue-500"
                  @click="closeModal"
                >
                  No
                </button>
              </div>
            </div>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script>
import { ref } from 'vue';
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogOverlay,
  DialogTitle,
} from '@headlessui/vue';

export default {
  name: 'Task',
  props: {
    task: Object,
  },
  components: {
    TransitionRoot,
    TransitionChild,
    Dialog,
    DialogOverlay,
    DialogTitle,
  },
  setup() {
    const isOpen = ref(false);
    // let curId;
    return {
      isOpen,
      // curId,
      closeModal() {
        isOpen.value = false;
      },
      openModal() {
        // curId = id;
        isOpen.value = true;
      },
    };
  },
  methods: {
    onDelete(id) {
      //   console.log(id);
      // isOpen.value = false;
      // console.log(curId);
      this.$emit('delete-task', id);
      this.closeModal();
    },
  },
};
</script>
