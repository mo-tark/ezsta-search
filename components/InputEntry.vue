
<template>
  <div>
    <div text-gray:80>Search for a EZSTA mapping file</div>
    <div flex justify-center>
      <div relative border="~ rounded base" shadow font-200 m="t-5" w-200 min-w-full md:min-w-0>
        <input min-w-full ref="input" v-model="searchWord" aria-label="Enter search word here.." w="80%"
          placeholder="Enter search word here.." type="text" autocomplete="off" p="x6 y4" bg-transparent border-none
          class="!outline-none" @keydown.enter="go" @input="go">
        <button v-if="searchWord" absolute flex right-2 w-10 top-2 bottom-2 text-xl op90 hover:op90 hover:color-red
          aria-label="Clear search" @click="clear()">
          <span i-carbon-close ma block aria-hidden="true" />
        </button>
      </div>
    </div>

    <button font-500 m-3 text-m uppercase btn :disabled="!searchWord" @click="go">
      Search
    </button>
    <button font-500 m-3 text-sm uppercase bg-bluegray hover-bg-yellow color-black btn @click="random">
      Show random File
    </button>

    <div>
      <!-- show the result of the search -->
      <div v-if="show">
        <!-- show Result componete for all resulst in resultfuse -->
        <Result v-for="(item) in resultfuse" :result="item"></Result>

      </div>
      <div v-else>
        No File found
      </div>

    </div>
  </div>
</template>


<script setup lang="ts">
import Fuse from 'fuse.js'


const searchWord = ref('')
const show = ref(true)
const loading = ref(false)
const { data } = await useFetch(() => `https://mo-tark.github.io/ezsta-list-api/mappings`)
let resultfuse = ref({})

let options = {
  includeScore: true,
  minMatchCharLength: 3,
  threshold: 0.4,
  keys: ['name', "description", "tags"]
}


let fuse = new Fuse(data._rawValue.mappings, options)

const clear = () => {
  searchWord.value = ''
  show.value = false
  resultfuse.value = {}
}
const random = () => {
  try {
    searchWord.value = data._rawValue.mappings[Math.floor(Math.random() * data._rawValue.mappings.length)].name
    go()
  }
  catch {
    return
  }
}

const go = () => {
  loading.value = true
  // show.value = !show.value
  if (searchWord.value) {
    // remove trailing whitespaces
    let search = searchWord.value.trim()
    resultfuse = fuse.search(search)
    if (resultfuse.length > 0) {
      show.value = true
    } else {
      show.value = false
    }

  }
  loading.value = false

}

</script>