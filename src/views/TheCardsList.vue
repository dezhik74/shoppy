<template>
  <div>
    <ul class="list__container">
      <cards-list-item
        v-for="card in getCardsData"
        :key="card.uid"
        :product="card"
      />
    </ul>
  </div>
</template>

<script>
import CardsListItem from '../components/CardsListItem.vue';

export default {
  name: 'TheCardsList',
  components: {
    CardsListItem,
  },
  props: {
    showFavorite: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    getCardsData: function () {
      return this.showFavorite
        ? this.$store.getters.getFilteredCardsData
        : this.$store.state.cardsData;
    },
  },
};
</script>
<style scoped>
.list__container {
  padding: 0;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  column-gap: 8px;
  row-gap: 8px;
}

@media (max-width: 1000px) {
  .list__container {
    grid-template-columns: repeat(3, 1fr);
  }
}
@media (max-width: 780px) {
  .list__container {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 500px) {
  .list__container {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
