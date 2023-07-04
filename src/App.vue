<template>
  <section class="card">
    <PopupCard v-model:isVisible="isVisible" :info="popupInfo" @newValue="newValue" />
    <div class="container">
      <h1>Cards List by t.me/lebowsski</h1>
      <ul class="card__list">
        <CardItem v-for="card in getCardList" :key="card.name" :card="card" @showPopup="showPopup" />
      </ul>
    </div>
  </section>
</template>

<script>
import CardItem from '@/components/CardItem.vue'
import PopupCard from '@/components/PopupCard.vue'
import { mapGetters } from 'vuex';

export default {
  name: 'App',
  data() {
    return {
      isVisible: false,
      popupInfo: {}
    }
  },
  components: {
    CardItem,
    PopupCard
  },
  methods: {
    showPopup(name) {
      this.isVisible = true
      this.popupInfo = this.getCardList.find(item => item.name === name)
    },
    newValue(info) {
     this.$store.commit('changeCardList',{value:info.value,name:info.name})
    }
  },
  computed: {
    ...mapGetters(['getCardList'])
  }
}
</script>

<style>
*,
*::after,
*::before {
  -webkit-box-sizing: inherit;
  box-sizing: inherit;
}

ul,
ol {
  padding: 0;
}

body,
h1,
h2,
h3,
h4,
h5,
h6,
p,
ul,
ol,
li,
figure,
figcaption,
blockquote,
dl,
dd {
  margin: 0;
}

ul[class] {
  list-style: none;
}

img {
  max-width: 100%;
  display: block;
}

input,
button,
textarea,
select {
  font: inherit;
}

a {
  text-decoration: none;
  font: inherit;
  display: inline-block;
}

body {
  min-height: 100vh;
  font-family: Montserrat, sans-serif;
  font-style: normal;
  font-size: 16px;
  color: black;
  background-color: gainsboro;
}

.card {
  padding: 50px 0;
  text-align: center;
}

h1 {
  padding-bottom: 40px;
  font-size: 36px;
}

.container {
  max-width: 920px;
  padding: 0 10px;
  margin: 0 auto;
}

.card__list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
}
</style>
