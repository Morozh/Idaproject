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
  data() {
    return {
      cards: [
        {
          id: 1,
          title: 'Наименование товара 1',
          img: 'https://root-nation.com/wp-content/uploads/2021/03/nikon-z-5-01.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
        {
          id: 2,
          title: 'Наименование товара 2',
          img: 'https://root-nation.com/wp-content/uploads/2021/03/nikon-z-5-01.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
        {
          id: 3,
          title: 'Наименование товара 3',
          img: 'https://root-nation.com/wp-content/uploads/2021/03/nikon-z-5-01.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
        },
      ],
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

.card-enter, .card-leave-to {
  opacity: 0;
  transform: translateY(-10px);

  @include respondTo(mobile) {
    transform: translateY(0) translateX(-10px);
  }
}

</style>
