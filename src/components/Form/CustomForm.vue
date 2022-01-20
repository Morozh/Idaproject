<template>
  <form
    class="form"
    novalidate
    @submit.prevent="sendData"
  >
    <div class="form__body">
      <div class="form__row">
        <custom-input
          v-model.trim="form.productName"
          label="Наименование товара"
          placeholder="Введите наименование товара"
          :required="true"
          :hasError="v$.form.productPrice.$error"
          @change="checkEmpty(productName)"
        />
      </div>

      <div class="form__row">
        <custom-textarea
          v-model="form.productDescription"
          label="Описание товара"
          placeholder="Введите описание товара"
          @change="checkEmpty(productDescription)"
        />
      </div>

      <div class="form__row">
        <custom-input
          v-model.trim="form.productImgLink"
          label="Ссылка на изображение товара"
          placeholder="Введите ссылку"
          :required="true"
          :hasError="v$.form.productPrice.$error"
          @change="checkEmpty(productImgLink)"
        />
      </div>

      <div class="form__row">
        <custom-input
          v-model.trim="form.productPrice"
          label="Цена товара"
          placeholder="Введите цену"
          :required="true"
          :hasError="v$.form.productPrice.$error"
          @change="checkEmpty(productPrice)"
        />
      </div>
    </div>
    <div class="form__footer">
      <custom-button
        :disabled="blockSubmit && v$.$invalid"
        type="submit"
      >
        <template v-slot:text>
          <span>Добавить товар</span>
        </template>
      </custom-button>
    </div>
  </form>
</template>

<script>
import useValidate from '@vuelidate/core';
import { required } from '@vuelidate/validators';
import CustomInput from '@/components/UI/Input/CustomInput.vue';
import CustomTextarea from '@/components/UI/Textarea/CustomTextarea.vue';
import CustomButton from '@/components/UI/Button/CustomButton.vue';

export default {
  name: 'CustomForm',
  components: {
    CustomInput,
    CustomTextarea,
    CustomButton,
  },
  data() {
    return {
      form: {
        productName: '',
        productDescription: '',
        productImgLink: '',
        productPrice: '',
      },
      v$: useValidate(),
      blockSubmit: true,
      cardsData: [],
    };
  },
  validations() {
    return {
      form: {
        productName: { required },
        productImgLink: { required },
        productPrice: { required },
      },
    };
  },
  methods: {
    checkEmpty(value) {
      this.blockSubmit = false;

      if (value === '') {
        this.blockSubmit = true;

        return true;
      }

      return false;
    },
    sendData() {
      this.v$.$touch();

      if (this.v$.form.$error) {
        alert('Не все поля корректно заполнены');
      } else {
        const data = {
          id: this.cardsData.length,
          title: this.form.productName,
          img: this.form.productImgLink,
          description: this.form.productDescription,
          price: this.form.productPrice,
        };

        this.cardsData.push(data);
        this.$emit('sendData', this.cardsData);
        localStorage.setItem('cards', JSON.stringify(this.cardsData));

        alert('Товар успешно добавлен!');

        this.form.productName = '';
        this.form.productImgLink = '';
        this.form.productDescription = '';
        this.form.productPrice = '';
        this.blockSubmit = true;
        this.v$.$reset();
      }
    },
  },
  mounted() {
    const parsedLocalStorage = JSON.parse(localStorage.cards);
    this.cardsData = parsedLocalStorage;
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
