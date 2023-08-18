<script setup>
import Card from './Card.vue';
import {reactive, ref,  watch} from 'vue'

const current = reactive({
  'value':1
})
const total = reactive({
  'value':1
})

const data = ref({})
const error = ref([])

let api = 'http://flems.github.io/test/api/news/';

function getData(page) {
fetch(`${api}${page}`)
    .then((res) => res.json())
    .then((json) => { data.value = json;
      total.value=data.value.nav.total;
    })
    .catch((err) => (error.value = err))
}

watch(current, () => {
  getData(current.value)
});

getData(current.value);

</script>
<template>
  <section class="news">
    <div class="news__flex">
        <Card v-for="newsItem in data.items" :newsItem="newsItem"/>
    </div>
    <div class="news__button-container">
      <button v-show="(current.value<total.value)" @click="current.value+=1" class="news__button">загрузить ещё</button>
    </div>
  </section>
</template>

<style scoped>
  .news {padding:64px 100px 72px 100px;}
  .news__flex {display:flex;flex-wrap:wrap;gap:64px 46px;margin-bottom:72px;}
  .news__button-container {display:flex;justify-content:center;}
  .news__button {cursor:pointer;display:inline-block;font-size:20px;font-weight:600;line-height:24px;letter-spacing:-0.01em;text-align:center;padding:16px 32px;border:1px solid #002DBF;border-radius:8px;background-color:white;color:#002DBF;}
</style>