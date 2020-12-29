<template>
  <div class="container">
    <div class="block" :class="{ animate: anival }"></div>
    <button @click="animateme">Animate</button>
  </div>
  <div class="container">
    <transition
      :css="false"
      @enter="enter"
      @after-enter="afterenter"
      @before-leave="beforeleave"
      @leave="leave"
      @after-leave="afterleave"
      @before-enter="beforeenter"
    >
      <p v-if="paracontrol">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Incidunt
        impedit fugiat quam molestias, excepturi soluta? Laudantium ullam sit
        magnam accusamus. Sunt totam fugiat doloribus, fugit corporis nemo
        facilis hic dolor.
      </p>
    </transition>
    <button @click="paracontrl">show / hide</button>
  </div>
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <transition name="on-button" mode="out-in">
      <button @click="showbutton" v-if="buttonval">show</button>
      <button @click="hidebutton" v-else>hide</button>
    </transition>
  </div>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>

  <div class="container">
    <listanimation />
  </div>
</template>  

<script>
import listanimation from './components/listanimation.vue';
export default {
  components: {
    listanimation,
  },
  data() {
    return {
      dialogIsVisible: false,
      anival: false,
      paracontrol: false,
      buttonval: true,
    };
  },
  methods: {
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateme() {
      this.anival = !this.anival;
    },
    paracontrl() {
      this.paracontrol = !this.paracontrol;
    },
    showbutton() {
      this.buttonval = false;
    },
    hidebutton() {
      this.buttonval = true;
    },
    beforeenter(el) {
      console.log('before Enter');
      el.style.opacity = 0;
      el.style.color = '#eee';
      // done();
    },
    enter(el, done) {
      console.log('enter');
      el.style.color = 'black';
      let count = 0;
      const counter = setInterval(() => {
        el.style.opacity = 0.01 * count;
        count += 10;
        if (count == 100) {
          clearInterval(counter);
          done();
        }
      }, 75);
    },
    beforeleave(el) {
      console.log('before leave', el);
    },
    leave(el, done) {
      console.log('leave');
      let count = 100;
      const counter = setInterval(() => {
        el.style.opacity = 0.01 * count;
        count -= 10;
        if (count == 0) {
          clearInterval(counter);
          done();
        }
      }, 75);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
/* p {
  animation: paraanimation 0.7s ease-in forwards;
  /* animation: name duration timing-function delay iteration-count direction fill-mode;} */
/* from vue animation */
/* .para-enter-from {
  opacity: 0%;
  transform: translateY(-3px) scale(0.7);
}
.para-enter-active {
  transition: all 0.5s;
}
.para-enter-to {
  opacity: 100%;
  transform: translateY(0) scale(1);
}

.para-leave-from {
  opacity: 100%;
  transform: translateY(0) scale(1);
}
.para-leave-active {
  transition: all 0.5s;
}
.para-leave-to {
  opacity: 0%;
  transform: translateY(-3px) scale(0.8);
} */

.on-button-enter-from,
.on-button-leave-to {
  opacity: 0;
}
.on-button-enter-to,
.on-button-leave-from {
  opacity: 1;
}
.on-button-enter-active {
  transition: all 0.3s ease-out;
}

.on-button-leave-active {
  transition: all 0.3s ease-in;
}
/* vue animation */

body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
  border: none;
  outline: none;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition: transform 0.4s ease-in; */
  /* transition: all 0.2s; */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
  outline: none;
}
.animate {
  animation: move-left 0.4s ease-in-out 100 forwards;
  /* background: #000; */
}
@keyframes paraanimation {
  from {
    opacity: 0;
    transform: translateX(2px) scale(0.7);
  }
  to {
    opacity: 100%;
    transform: translateX(0px) scale(1);
  }
}

@keyframes move-left {
  0% {
    transform: translateX(0) scale(1);
  }
  50% {
    transform: translateX(130px) scale(1.2);
  }
  100% {
    transform: translateX(150px) scale(1);
  }
}
</style>