<script setup>
  import moment from 'moment';
  const props = defineProps({
    newsItem: Object
  });

  const humanDate =  new Date(props.newsItem.date * 1000);
  const dateDay = moment(humanDate).format('DD');
  const dateMonth = moment(humanDate).format('MMMM');
  const dateYear = moment(humanDate).format('YYYY');

  const parcedText = props.newsItem.previewText
  const cleanedText = parcedText.replace(/\&nbsp;/g, " ");

</script>

<template>
  <section class="card">
    <div v-show="newsItem.image" class="card__img-container">
        <img class="card__img" :src="newsItem.image" alt="News image">
    </div>
    <div class="card__container">
      <div v-show="newsItem.image" style="height:250px;flex-shrink:0"></div>
      <div v-show="!newsItem.image" style="height: 16px;"></div>
      <div class="card__date">
        <div>
          <span class="card__date-day" >{{ dateDay }}</span>
        </div>
        <div>
          <span class="card__date-rest">{{ dateMonth }}</span>
          <span class="card__date-rest">{{ dateYear }}</span>
        </div>
      </div>
      <h4>{{ newsItem.name }}</h4>
      <p>{{ cleanedText }}</p>
    </div>
    <div class="card__badge-container">
      <div class="card__badge">{{ newsItem.type.value}}</div>
    </div>
  </section>
</template>

<style scoped>
.card {position:relative;cursor:pointer}
.card:hover h4 {color:#0029A9}
.card__container {width:536px;height:577px;border:1px solid #0F62FE;border-radius:16px;display:flex;flex-direction:column;padding:32px;overflow:hidden}
.card__img-container {width:536px;height:250px;border-radius:16px 16px 0px 0px; position:absolute;top:-1px}
.card__img {width:100%;height:auto;border-radius:16px 16px 0px 0px}
.card__date {margin-bottom:16px;display:flex;color:#A1A7B5}
.card__date-day {font-size:36px;font-weight:400;line-height:36px;letter-spacing:0em;text-align:left}
.card__date-rest {margin-left:4px;display:block;font-size:15px;font-weight:700;line-height:17px;letter-spacing:-0.01em;text-align:left}
.card__badge-container {position:absolute;bottom:1px;left:2px;padding:0 32px;height:92px;width:530px;background-color:white;
display:flex;align-items:center;border-radius:16px;border:2px solid transparent}
.card__badge {padding:4px 16px 4px 16px;border-radius:360px;background-color:#F0F6FE}
.card h4 {display:block;font-size:22px;font-weight:400;line-height:26px;letter-spacing:0em;text-align:left;color:#0C5BEF;margin-bottom:16px}
.card p {display:block;font-size:20px;font-weight:400;line-height:26px;letter-spacing:-0.01em;text-align:left;flex-shrink:1}
</style>