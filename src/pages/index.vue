<script setup lang="ts">
/* eslint-disable no-console */
const prefixID = 'testList'
const people = [
  { name: 'User 1', age: 20 },
  { name: 'User 2', age: 30 },
  { name: 'User 3', age: 40 },
  { name: 'User 4', age: 50 },
]

const reactPeople = ref(Object.assign([], people))

function reset() {
  reactPeople.value = Object.assign([], people)
}

function remove() {
  reactPeople.value.splice(1, 1)
}

function mark() {
  for (const i of [0, 1]) {
    const elem = document.getElementById(prefixID + i)
    elem.children[1]?.classList.toggle('bg-green')
  }
}

const prevHTML = ['', '']

function logDomOnChange() {
  for (const i of [0]) {
    const elem = document.getElementById(prefixID + i)
    if (!elem)
      return
    if (prevHTML[i] !== elem.innerHTML) {
      console.log(i, '===== Updated ==========', elem.innerHTML)
      prevHTML[i] = elem.innerHTML
    }
  }
}

const { pause, resume } = useRafFn(() => {
  logDomOnChange()
})
</script>

<template>
  <button btn m-3 @click="reset">
    Reset
  </button>
  <button btn m-3 @click="remove">
    Remove second
  </button>
  <button btn m-3 @click="mark">
    Mark second
  </button>
  <br>
  List with :key="index"
  <br m-3>
  <ul :id="prefixID + 0">
    <li v-for="(person, index) in reactPeople" :key="index">
      {{ person.name }} - {{ index }}
    </li>
  </ul>
  <br m-3>
  List with :key="person.name":
  <br m-3>
  <ul :id="prefixID + 1">
    <li v-for="(person, index) in reactPeople" :key="person.name">
      {{ person.name }} - {{ index }}
    </li>
  </ul>
</template>

