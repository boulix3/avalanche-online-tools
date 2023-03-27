<script setup lang="ts">
import { BinTools } from "@avalabs/avalanchejs"
import { Buffer } from 'buffer/'

import { reactive } from "vue";
function onKeyup(event: KeyboardEvent) {
  console.log('key up', event)
  state.vmId = convertCB58ToString(state.inputText)
}
function convertCB58ToString(input: string): string {
  var bt = BinTools.getInstance();
  let inputBuff = Buffer.alloc(32)
  inputBuff.write(input)
  const result = bt.cb58Encode(inputBuff)
  return result.toString()
}

const state = reactive({ vmId: '', inputText: '' })

</script>

<template>
  <div class="home">
    <h1>VmIdBuilder Page</h1>
    <h3>Type the vm name to get the corresponding VMId</h3>
    <input v-model="state.inputText" @keyup="onKeyup($event)" debounce="500">
    <p>The vm id is : </p>
    <p>{{ state.vmId }}</p>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
