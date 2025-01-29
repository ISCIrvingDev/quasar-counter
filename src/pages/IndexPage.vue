<template>
  <q-page class="flex flex-center text-white" v-touch-pan.vertical.prevent.mouse="handlePan">
    <div class="row">
      <q-input
        type="text"
        placeholder="Counter"
        v-model="data.name"
        input-class="text-center text-h5 text-white"
        color="teal"
        filled
      />
    </div>

    <div class="row full-width items-center">
      <div class="col text-center">
        <q-btn
          round
          icon="remove"
          size="xl"
          @click="decreaseCounter"
          v-touch-repeat:0:100.mouse.enter.space="decreaseCounter"
        />
      </div>

      <div class="col text-center text-h2">
        {{ data.counter }}
      </div>

      <div class="col text-center">
        <q-btn
          round
          icon="add"
          size="xl"
          @click="increaseCounter"
          v-touch-repeat:0:100.mouse.enter.space="increaseCounter"
        />
      </div>
    </div>

    <div class="row">
      <q-btn round icon="restart_alt" size="xl" @click="resetCounter" />
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { useQuasar } from 'quasar'
import { reactive, watch } from 'vue'

/*
  Storage
*/
const $q = useQuasar()

/*
  Variables
*/
const data = reactive({
  counter: 0,
  name: '',
})
const savedData = $q.localStorage.getItem('counter')

/*
  Al iniciar la app
*/
watch(data, (value) => {
  $q.localStorage.set('counter', value)
})

if (savedData) Object.assign(data, savedData)

/*
  Metodos
*/
const increaseCounter = () => {
  data.counter++
}
const decreaseCounter = () => {
  if (data.counter > 0) data.counter--
}
const resetCounter = () => {
  data.name = ''
  data.counter = 0
}
// eslint-disable-next-line @typescript-eslint/no-explicit-any
const handlePan = (e: any) => {
  console.log(e.delta.y)
  if (e.delta.y < 0) increaseCounter()
  else decreaseCounter()
}
</script>

<style scoped>
.q-page {
  max-width: 700px;
  margin: 0 auto;
}
</style>
