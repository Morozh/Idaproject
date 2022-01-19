<template>
  <div class="main">
    <div class="main__wrapper">
      <div class="main__layout">
        <div class="main__layout-col">
          <h1 class="main__title">Добавление товара</h1>

          <custom-form />
        </div>

        <div class="main__layout-col">
          <p>Карточки</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CustomForm from '@/components/Form/CustomForm.vue';

export default {
  name: 'App',
  components: {
    CustomForm,
  },
};
</script>

<style lang="scss" src="./assets/scss/main.scss" />
