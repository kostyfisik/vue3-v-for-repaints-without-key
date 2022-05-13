<script setup lang="ts">
const people = [
  { name: 'User 1', age: 20 },
  { name: 'User 2', age: 30 },
  { name: 'User 3', age: 40 },
]

const reactPeople = ref(people)

function reset() {
  reactPeople.value = [
    { name: 'User 1', age: 20 },
    { name: 'User 2', age: 30 },
    { name: 'User 3', age: 40 },
  ]
}

function remove() {
  reactPeople.value.splice(1, 1)
}

let prevHTML = ''

function logDomOnChange() {
  const elem = document.getElementById('testList')
  if (!elem)
    return
  if (prevHTML !== elem.innerHTML) {
    console.log('========= OLD ==========', prevHTML)
    console.log('    ===== NEW ==========', elem.innerHTML)
    prevHTML = elem.innerHTML
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
  <br>
  List:
  <br m-3>
  <ul id="testList">
    <li v-for="(person, index) in reactPeople" :key="index">
      {{ person.name }} - {{index}}
    </li>
  </ul>
</template>

