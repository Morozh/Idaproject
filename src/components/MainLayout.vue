<template>
  <div class="main">
    <div class="main__wrapper">
      <div class="main__layout">
        <div class="main__layout-col">
          <h1 class="main__title">{{ title }}</h1>

          <div class="main__form">
            <custom-form />
          </div>
        </div>
        <div class="main__layout-col">
          <div class="main__catalog">
            <catalog />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CustomForm from '@/components/Form/CustomForm.vue';
import Catalog from '@/components/Catalog/Catalog.vue';

export default {
  name: 'MainLayout',
  components: {
    CustomForm,
    Catalog,
  },
  data() {
    return {
      title: 'Добавление товара',
    };
  },
};
</script>

<style lang="scss" scoped>
.main {
  font-size: 16px;
  line-height: 20px;
  padding: 32px 0;

  &__wrapper {
    max-width: 1440px;
    margin: 0 auto;
    padding: 0 32px;
  }

  &__layout {
    display: flex;
    justify-content: space-between;

    @include respondTo(tablet) {
      flex-direction: column;
    }

    &-col {
      flex-basis: 100%;

      &:first-of-type {
        max-width: 332px;
        margin-right: 16px;

        @include respondTo(tablet) {
          max-width: unset;
          margin-right: 0;
          margin-bottom: 24px;
        }
      }
    }
  }

  &__title {
    font-size: 28px;
    line-height: 35px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  &__form {
    position: sticky;
    top: 24px;
  }
}
</style>
