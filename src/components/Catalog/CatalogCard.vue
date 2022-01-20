<template>
  <div class="catalog-card">
    <div
      class="catalog-card__delete"
      @click="deleteCardRequest"
    >
      <img src="@/assets/img/trashcan.svg" alt="Удалить" />
    </div>
    <div class="catalog-card__img">
      <img :src="cardData.img" alt="Фото" />
    </div>
    <div class="catalog-card__content">
      <h3 class="catalog-card__title">{{ cardData.title }}</h3>
      <p class="catalog-card__description">
        {{ cardData.description }}
      </p>
      <span class="catalog-card__price">{{ cardData.price }} руб.</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CatalogCard',
  props: {
    cardData: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  data() {
    return {};
  },
  methods: {
    deleteCardRequest() {
      this.$emit('deleteCard', this.cardData.id);
    },
  },
};
</script>

<style lang="scss" scoped>
.catalog-card {
  position: relative;
  border-radius: 4px;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  background-color: $color-primary;
  display: flex;
  flex-direction: column;
  cursor: pointer;
  transition: all .3s;

  &:hover {
    .catalog-card__delete {
      opacity: 1;
      pointer-events: auto;
      visibility: visible;
      transform: translateY(0);
    }
  }

  &__img {
    width: 100%;
    min-height: 200px;
    max-height: 200px;
    overflow: hidden;
    border-radius: 4px 4px 0 0;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }

  &__content {
    padding: 16px 16px 24px 16px;
    color: $color-lighten-black;
  }

  &__title {
    font-size: 20px;
    line-height: 25px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  &__description {
    margin-bottom: 32px;
  }

  &__price {
    font-size: 24px;
    line-height: 30px;
    font-weight: 600;
  }

  &__delete {
    display: flex;
    justify-content: center;
    align-content: center;
    position: absolute;
    right: -8px;
    top: -8px;
    width: 32px;
    height: 32px;
    padding: 8px;
    border-radius: 10px;
    background-color: $color-pink;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    transition: all .3s;
    pointer-events: none;
    opacity: 0;
    visibility: hidden;
    transform: translateY(-20px);
  }
}

</style>
