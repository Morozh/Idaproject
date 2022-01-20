<template>
  <div
    class="catalog"
    :class="{'catalog_empty' : emptyCardsArr}"
  >

    <p
      v-if="emptyCardsArr"
      class="catalog__notice"
    >Список товаров пуст..</p>

    <transition-group name="card" v-else>
      <catalog-card
        v-for="card in cards"
        :key="card.id"
        :card-data="card"
        @deleteCard="deleteCardFromCatalog"
      />
    </transition-group>
  </div>
</template>

<script>
import CatalogCard from '@/components/Catalog/CatalogCard.vue';

export default {
  name: 'Catalog',
  components: {
    CatalogCard,
  },
  props: {
    data: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      cards: this.data,
    };
  },
  computed: {
    emptyCardsArr() {
      return this.cards.length < 1;
    },
  },
  methods: {
    deleteCardFromCatalog(cardId) {
      const cardToRemove = this.cards.find((card) => card.id === cardId);
      const cardIndex = this.cards.indexOf(cardToRemove);
      this.cards.splice(cardIndex, 1);
      localStorage.setItem('cards', JSON.stringify(this.cards));
    },
  },
  mounted() {
    const localStorageData = localStorage.getItem('cards');

    if (localStorageData !== '[]') {
      this.cards = JSON.parse(localStorageData);
    }
  },
  watch: {
    data(val) {
      this.cards = val;
    },
  },
};
</script>

<style lang="scss" scoped>
.catalog {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-top: 52px; // временно

  &_empty {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
  }

  @include respondTo(tablet) {
    grid-template-columns: repeat(2, 1fr);
  }

  @include respondTo(mobile) {
    grid-template-columns: repeat(1, 1fr);
  }

  &__notice {
    font-size: 30px;
    font-weight: 600;
    opacity: .5;
    transition: all .3s;
  }
}

.card-enter-active,
.card-leave-active {
  transition: all .3s;
}

.card-enter-to, .card-leave-to {
  opacity: 0;
  transform: translateY(10px);

  @include respondTo(mobile) {
    transform: translateY(0) translateX(10px);
  }
}

</style>
