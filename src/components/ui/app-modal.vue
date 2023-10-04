<template>
  <div class="app-modal" :class="{ 'app-modal-show': modelValue }">
    <app-transition>
      <div v-if="modelValue" class="app-modal__body">
        <slot></slot>
      </div>
    </app-transition>
  </div>
  <app-transition>
    <span
      @click="$emit('update:modelValue', false)"
      v-if="modelValue"
      class="app-modal-shadow"
    ></span>
  </app-transition>
</template>

<script setup>
  import AppTransition from "@/components/ui/app-transition.vue";
  const props = defineProps({
    modelValue: {
      type: Boolean,
      default: false,
    },
    width: {
      type: String,
    },
  });
</script>

<style lang="scss" scoped>
  .app-modal {
    color: black;
    position: fixed;
    transform: translate(-50%, -50%);
    left: 50%;
    width: 50%;
    max-height: 600px;
    top: 50%;
    // background-color: white;
    border-radius: 10px;
background: rgba(255, 255, 255, 0.29);
box-shadow: 0px -5px 60px 0px rgba(0, 0, 0, 0.50);
    z-index: -1;
    opacity: 0.2;
    overflow: auto;
    // border-radius: 0.5rem;
  }

  .app-modal-show {
    opacity: 1;
    z-index: 100;
  }

  ::-webkit-scrollbar {
    display: none;
  }

  .app-modal__body {
    padding: 20px;
  }

  .app-modal-shadow {
    // background-color: rgba(0, 0, 0, 0.5);
    background: rgba(0,0,0 ,0.5);

    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
  }

 
</style>
