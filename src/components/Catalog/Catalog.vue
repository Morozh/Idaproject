<template>
  <div class="catalog">
    <catalog-card />
    <catalog-card />
    <catalog-card />
    <catalog-card />
    <catalog-card />
    <catalog-card />
    <catalog-card />
    <catalog-card />
    <catalog-card />
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
    return {};
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

  @include respondTo(tablet) {
    grid-template-columns: repeat(2, 1fr);
  }

  @include respondTo(mobile) {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
