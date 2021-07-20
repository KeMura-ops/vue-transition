<template>
  <div class="main">
    <button @click="show = !show">切り替え</button>
    <!-- トランジションの使用には「transition」タグとnameを用意する -->
    <transition name="fade">
      <p v-if="show">hello</p>
    </transition>
     <!-- トランジションとアニメーションが両方使用したい場合typeで優先するものを指定できる -->
    <transition name="slide" type="animation">
      <p v-show="show">bye</p>
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
/* 切り替えの際にVue内部で「enter-active」や「enter-to」と言ったクラスを付けたり外したりしている */
.fade-enter {
  /* 現れる時の最初の状態 */
  opacity: 0;
}
.fade-enter-active {
  /* 現れる時のトランジションの状態 */
  transition: opacity 0.5s;
}
.fade-enter-to {
  /* 現れる時の最後の状態 */
  opacity: 1;
}
.fade-leave {
  /* 消える時の最初の状態 */
  opacity: 1;
}
.fade-leave-active {
  /* 消える時のトランジションの状態 */
  transition: opacity 0.5s;
}
.fade-leave-to {
  /* 消える時の最後の状態 */
  opacity: 0;
}

.slide-enter,
.slide-leave-to {
  opacity: 0;
}

/* CSSアニメーション */
/* アニメーションの場合キーフレームに効果を指定してあげればenterとleaveのアクティブに記述すれば良い */
.slide-enter-active {
  animation: slide-in 0.5s; /* キーフレームの名前を指定する */
  transition: opacity 1s; /* アニメーションにトランジションも指定する */
}
.slide-leave-active {
  animation: slide-in 0.5s reverse; /* reverseで逆の効果を与えている */
  transition: opacity 1s; /* アニメーションにトランジションも指定する */
}

/* CSSアニメーション キーフレーム */
@keyframes slide-in {
  from {
    transform: translateX(100px);
  }
  to {
    transform: translateX(0);
  }
}

.main {
  width: 70%;
  margin: 0 auto;
  padding-top: 5rem;
  text-align: center;
}
</style>