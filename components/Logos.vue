<template>
  <div inline-flex text-2xl font-300 cursor-default>
    <div flex flex-col children:mx-auto>
      <template v-if="$colorMode.value === 'light'">
        <img w-80 inline-block src="img/ezsta_logo.png">
        <span text-black mt-2>EZSTA Mapping Finder</span>
      </template>
      <template v-else>
        <img w-80 inline-block src="img/ezsta_logo_light.png">
        <span text-white mt-2>EZSTA Mapping Finder</span>
      </template>
    </div>
  </div>
</template>
