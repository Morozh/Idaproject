<template>
  <div
    class="catalog"
    :class="{'catalog_empty' : emptyCardsArr}"
  >

  <p
    v-if="emptyCardsArr"
    class="catalog__notice"
  >Список товаров пуст..</p>

  <div class="catalog__wrapper" v-else>
    <div class="catalog__wrapper-row">
      <div
        class="dropdown"
        @click="openDropdown"
      >
        <span class="dropdown__selected">{{ selected }}</span>
        <img
          class="dropdown__arrow"
          :class="{'is-opened': optionsVisible}"
          src="@/assets/img/arrow.svg"
          alt="Срелка"
        >

        <div
          class="dropdown__options"
          v-if="optionsVisible"
        >
          <span
            class="dropdown__option"
            v-for="option in options"
            :key="option"
            @click="sortBySelectedOption(option)"
          >
            {{ option.value }}
          </span>
        </div>
      </div>
    </div>
    <div class="catalog__wrapper-row grid">
      <transition-group name="card">
        <catalog-card
          v-for="card in cards"
          :key="card.id"
          :card-data="card"
          @deleteCard="deleteCardFromCatalog"
        />
      </transition-group>
    </div>
  </div>
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
      optionsVisible: false,
      options: [
        {
          value: 'По возрастанию',
          type: 'asc',
        },
        {
          value: 'По убыванию',
          type: 'desc',
        },
        {
          value: 'По наименованию',
          type: 'name',
        },
      ],
      selected: 'По умолчанию',
    };
  },
  computed: {
    emptyCardsArr() {
      return this.cards.length < 1;
    },
  },
  methods: {
    openDropdown() {
      this.optionsVisible = !this.optionsVisible;
    },
    sortBySelectedOption(option) {
      this.selected = option.value;

      if (option.type === 'asc') {
        this.cards.sort((a, b) => Number(a.price) - Number(b.price));
      } else if (option.type === 'desc') {
        this.cards.sort((a, b) => Number(b.price) - Number(a.price));
      } else if (option.type === 'name') {
        this.cards.sort((a, b) => {
          if (a.title < b.title) return -1;
          return a.title > b.title ? 1 : 0;
        });
      }
    },
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
.grid {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;

  @include respondTo(tablet) {
    grid-template-columns: repeat(2, 1fr);
  }

  @include respondTo(mobile) {
    grid-template-columns: repeat(1, 1fr);
  }
}

.catalog {
  width: 100%;
  height: 100%;

  &_empty {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
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

%dropdown-base {
  padding: 10px 16px;
  background: $color-primary;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.dropdown {
  @extend %dropdown-base;

  height: 36px;
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 142px;
  font-size: 12px;
  line-height: 15px;
  color: $color-dark-gray;
  cursor: pointer;
  margin-left: auto;
  margin-bottom: 16px;

  &__selected {
    margin-right: 4px;
  }

  &__arrow {
    transition: all .3s;
    margin-top: 1px;

    &.is-opened {
      transform: rotate(180deg);
    }
  }

  &__options {
    @extend %dropdown-base;

    position: absolute;
    left: 0;
    top: 42px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    white-space: nowrap;
    width: 100%;
    z-index: 100;
  }

  &__option {
    transition: color .3s;
    cursor: pointer;

    &:not(:last-of-type) {
      margin-bottom: 8px;
    }

    &:hover {
      color: $color-dark-purple;
    }
  }
}

</style>
