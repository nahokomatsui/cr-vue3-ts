<template>
  <header class="header">
    <h1>Vue 3 + TypeScript + Vite inspired「基礎から学ぶ Vue.js」</h1>
  </header>

  <div class="container">
    <side class="menu">
      <ul>
        <li v-for="(menu, index) in menuList">
          <button
            :class="Number(index) === activeMenu ? 'is-active' : ''"
            @click="changeMenu(Number(index))"
          >
            {{ menu }}
          </button>
        </li>
      </ul>
    </side>

    <main class="main">
      <template v-if="activeMenu === 0">
        <img alt="Vue logo" src="./assets/logo.png" />
        <HelloWorld />
      </template>

      <template v-else>
        <component :is="menuFunc(activeMenu)" />
      </template>
    </main>
  </div>
</template>

<script setup lang="ts">
import { defineComponent, readonly, ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Chapter1 from './components/Chapter1.vue'
import Chapter2 from './components/Chapter2.vue'
import Chapter3 from './components/Chapter3.vue'
import Chapter4 from './components/Chapter4.vue'
import Chapter5 from './components/Chapter5.vue'

defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    Chapter1,
    Chapter2,
    Chapter3,
    Chapter4,
    Chapter5,
  },
})

type Chapter = typeof Chapter1
  | typeof Chapter2
  | typeof Chapter3
  | typeof Chapter4
  | typeof Chapter5

const menuList = readonly({
  1: 'CHAPTER 1',
  2: 'CHAPTER 2',
  3: 'CHAPTER 3',
  4: 'CHAPTER 4',
  5: 'CHAPTER 5',
})
const activeMenu = ref(0)

const changeMenu = (menu: number): void => {
  activeMenu.value = menu
}
const menuFunc = (menu: number): Chapter | undefined => {
  let chapter: Chapter | undefined
  switch (menu) {
    case 1: chapter = Chapter1
      break
    case 2: chapter = Chapter2
      break
    case 3: chapter = Chapter3
      break
    case 4: chapter = Chapter4
      break
    case 5: chapter = Chapter5
      break
    default: chapter = undefined
  }
  return chapter
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>

<style lang="scss" scoped>
.header {
  padding: 0 2rem;
}
.container {
  display: flex;
}
.menu {
  position: relative;
  width: 30%;

  ul {
    position: fixed;
    list-style: none;
    padding: 0 2rem 2rem;

    li {
      margin: 1rem;
    }

    button {
      color: #2c3e50;
      font-size: 1rem;
      font-weight: bold;
      border: none;
      outline: none;
      background-color: white;

      &:hover {
        cursor: pointer;
      }
      &.is-active {
        color: #3eaf7c;
      }
    }
  }
}
</style>
