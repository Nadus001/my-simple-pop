<script setup>
import { ref } from 'vue'
import style from 'index.module.css'
import data from 'src/components/listI/dt.js'

defineProps({
  msg: String,
})

let count = ref(0)

function culcScrore(value) {
  count += value;
}
</script>

<template>

</template>

