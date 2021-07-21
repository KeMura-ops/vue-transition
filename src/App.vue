<template>
  <div class="main">
    <button @click="myAnime = 'slide'">Slide</button>
    <button @click="myAnime = 'fade'">Fade</button>
    <p>{{ myAnime }}</p>
    <button @click="show = !show">切り替え</button>
    <hr>
    <button @click="myCom = 'ComponentA'">ComponentA</button>
    <button @click="myCom = 'ComponentB'">ComponentB</button>
    <transition name="fade" mode="out-in">
      <component :is="myCom"></component>
    </transition>
    <transition name="fade" mode="out-in"> <!-- mode属性を使用することでトランジションを滑らかにできる -->
      <!-- v-showは単発のものにしか使用できないため、複数の場合はv-ifなどを使用する -->
      <!-- トランジションの中で複数の要素を使用する場合は、タグを判別するためにkey属性を付けると良い -->
      <p v-if="show" key="bye">Good Bye</p>
      <p v-else key="hello">Good Afternoon</p>
    </transition>
    <transition
      enter-active-class="animate__animated animate__bounce"
      leave-active-class="animate__animated animate__flash"
      appear=""
    > <!-- 
        enter...,leave...でクラス名を上書きできる
        これを利用してanimate.cssのクラスを指定すると
        その効果を適用できる(カスタムトランジション) 
      -->
      <p v-if="show">hello</p>
    </transition>
    <!-- v-bindでトランジションを動的に切り替える -->
    <transition :name="myAnime" appear="">
      <p v-show="show">bye</p>
    </transition>
  </div>
</template>

<script>
import ComponentA from "./components/componentA.vue"
import ComponentB from "./components/componentB.vue"

export default {
  components: {
    ComponentA,
    ComponentB
  },
  data() {
    return {
      show: true,
      myAnime: 'slide', // 動的トランジションの初期値
      myCom: 'ComponentA'
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