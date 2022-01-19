<template>
  <div class="catalog-card">
    <div class="catalog-card__img">
      <img src="https://root-nation.com/wp-content/uploads/2021/03/nikon-z-5-01.jpg" alt="Фотоаппарат" />
    </div>
    <div class="catalog-card__content">
      <h3 class="catalog-card__title">Наименование товара</h3>
      <p class="catalog-card__description">
        Довольно-таки интересное описание товара в&nbsp;несколько строк.
        Довольно-таки интересное описание товара в&nbsp;несколько строк.
      </p>
      <span class="catalog-card__price">10 000 руб.</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CatalogCard',
};
</script>

<style lang="scss" scoped>
.catalog-card {
  position: relative;
  overflow: hidden;
  border-radius: 4px;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  background-color: $color-primary;
  display: flex;
  flex-direction: column;
  cursor: pointer;

  &__img {
    width: 100%;
    min-height: 200px;
    max-height: 200px;

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
}
</style>
