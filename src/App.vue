<template>
  <div class="main">
    <button @click="show = !show">切り替え</button>
    <!-- トランジションの使用には「transition」タグとnameを用意する -->
    <transition name="fade">
      <p v-if="show">hello</p>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: true
    }
  }
}
</script>

<style scoped>
/* トランジションのnameにenter...,leave...を付随した6つのトランジションクラスを記述する */
.fade-enter {}
.fade-enter-active {}
.fade-enter-to {}
.fade-leave {}
.fade-leave-active {}
.fade-leave-to {}

.main {
  width: 70%;
  margin: 0 auto;
  padding-top: 5rem;
  text-align: center;
}
</style>