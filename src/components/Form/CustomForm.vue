<template>
  <form class="form" action @submit.prevent>
    <div class="form__body">
      <div class="form__row">
        <custom-input
          v-model="productName"
          label="Наименование товара"
          placeholder="Введите наименование товара"
          required="true"
        />
      </div>

      <div class="form__row">
        <custom-textarea
          v-model="productImgLink"
          label="Описание товара"
          placeholder="Введите описание товара"
          required="false"
        />
      </div>

      <div class="form__row">
        <custom-input
          v-model="productImgLink"
          label="Ссылка на изображение товара"
          placeholder="Введите ссылку"
          required="true"
        />
      </div>

      <div class="form__row">
        <custom-input
          v-model="productPrice"
          label="Цена товара"
          placeholder="Введите цену"
          required="true"
        />
      </div>
    </div>
    <div class="form__footer">
      <custom-button
        :disabled="disabled"
      >
        <template v-slot:text>
          <span>Добавить товар</span>
        </template>
      </custom-button>
    </div>
  </form>
</template>

<script>
import CustomInput from '@/components/UI/Input/CustomInput.vue';
import CustomTextarea from '@/components/UI/Textarea/CustomTextarea.vue';
import CustomButton from '@/components/UI/Button/CustomButton.vue';

export default {
  name: 'App',
  components: {
    CustomInput,
    CustomTextarea,
    CustomButton,
  },
};
</script>

<style lang="scss" scoped>
.form {
  width: 100%;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  background-color: $color-primary;

  &__row {
    &:not(:last-of-type) {
      margin-bottom: 16px;
    }
  }

  &__body {
    margin-bottom: 24px;
  }
}
</style>
