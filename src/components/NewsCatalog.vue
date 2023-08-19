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

let api = 'https://flems.github.io/test/api/news/';

const newsArr = ref([]);


function getData(page) {
fetch(`${api}${page}`)
    .then((res) => res.json())
    .then((json) => { data.value = json;
      total.value=data.value.nav.total;
      newsArr.value = [...newsArr.value, ...data.value.items];
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
    <div class="news__grid">
      <div v-for="newsItem in newsArr" class="news__grid-cell">
        <Card  :newsItem="newsItem"/>
      </div>
    </div>
    <div class="news__button-container">
      <button v-show="(current.value<total.value)" @click="current.value+=1" class="news__button">загрузить ещё</button>
    </div>
  </section>
  
</template>

<style scoped>
  .news {padding:64px 100px 72px 100px;display: flex; flex-direction: column; align-items: center; }
  .news__grid {width: 100%;display: grid;grid-template-columns: 1fr 1fr 1fr;gap: 64px 48px;}
  @media (max-width: 1900px) {.news__grid {grid-template-columns: 1fr 1fr;gap: 44px 28px;}}
  @media (max-width: 1280px) {.news__grid {grid-template-columns: 1fr;}}
  .news__grid-cell {display: flex;justify-content: center;align-items: center;}
  .news__button-container {display:flex;justify-content:center;margin-top: 72px;}
  .news__button {cursor:pointer;display:inline-block;font-size:20px;font-weight:600;line-height:24px;letter-spacing:-0.01em;text-align:center;padding:16px 32px;border:1px solid #002DBF;border-radius:8px;background-color:white;color:#002DBF;}
</style>

<!-- <template>
  <section class="news">
    <div class="news__flex">
        <Card v-for="newsItem in newsArr" :newsItem="newsItem"/>
    </div>
    
  </section>
  <div class="news__button-container">
      <button v-show="(current.value<total.value)" @click="current.value+=1" class="news__button">загрузить ещё</button>
    </div>
</template>

<style scoped>
  .news {padding:64px 100px 72px 100px;display: flex; flex-direction: column; align-items: center; }
  
  .news__flex {display:flex;flex-wrap:wrap;gap:64px 48px;margin-bottom:72px;max-width: 1704px;}
  @media (max-width: 1900px) {
    .news__flex {justify-content: space-around;}
  }
  .news__button-container {display:flex;justify-content:center;}
  .news__button {cursor:pointer;display:inline-block;font-size:20px;font-weight:600;line-height:24px;letter-spacing:-0.01em;text-align:center;padding:16px 32px;border:1px solid #002DBF;border-radius:8px;background-color:white;color:#002DBF;}
</style> -->