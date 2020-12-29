<template>
  <div>
    <ul>
      <transition-group tag="ul" name="user-list">
        <li v-for="data in arraydata" :key="data" @click="remove(data)">
          {{ data }}
        </li>
      </transition-group>
    </ul>
    <input
      placeholder="type and press enter"
      type="text"
      name="data"
      id="data"
      @keydown.enter="addtoarray"
      v-model="dataone"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataone: '',
      arraydata: ['rahul', 'krishna', 'sai', 'dhandikatla'],
    };
  },
  methods: {
    addtoarray() {
      this.arraydata.unshift(this.dataone);
      this.dataone = '';
    },
    remove(data) {
      console.log(data);
      this.arraydata = this.arraydata.filter((val) => val !== data);
    },
  },
};
</script>

<style lang="css" scoped>
ul {
  list-style: none;
  margin: 2px;
  padding: 2px;
}

li {
  border: 1px solid grey;
  text-align: center;
  margin: 9px;
  cursor: not-allowed;
}

.user-list-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}
.user-list-leave-to {
  opacity: 0;
  transform: translateX(70px);
}
.user-list-enter-active {
  transition: all 0.1s ease-out;
}
.user-list-enter-to {
  opacity: 1;
  transform: translateX(0px);
}

.user-list-leave-active {
  transition: all 1s ease-in;
  position: absolute;
}

.user-list-move {
  transition: all 1s ease;
}
</style>