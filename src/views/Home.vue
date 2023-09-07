<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script>
import { ref } from "vue";
import Toast from "../components/Toast";
import Todos from "../components/Todos";

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false);
    const showP = ref(false);
    const toggleShowP = () => {
      showP.value = !showP.value;
    };
    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };

    return { showToast, triggerToast, showP, toggleShowP };
  },
};
</script>

<style>
.toast-leave-to {
  opacity: 0;
  transform: translateY(-100px) scale(0.7);
}
.toast-leave-from {
  opacity: 1;
  transform: translateY(0) scale(1);
}
.toast-leave-active{
  transition: all 0.5s ease-in-out;
}
.toast-enter-active {
  animation: shake 0.5s ease-in-out forwards;
}
@keyframes shake {
  0% {
    transform: translateY(-100px) scale(0.7);
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
  60% {
    transform: translateX(18px);
  }
  70% {
    transform: translateX(-18px);
  }
  80% {
    transform: translateX(10px);
  }
  90% {
    transform: translateX(-10px);
  }
  100% {
    transform: translateX(0);
  }
}
</style>
