<template>
  <div class="input-field">
    <label
      class="input-field__label"
      :class="{ 'input-field__label_required': this.required }">{{ label }}</label>
    <input
      v-model="inputValue"
      class="input-field__field"
      type="text"
      :placeholder="placeholder"
      :class="classes"
      :required="required"
    />
    <span class="input-field__msg" v-show="hasError">{{ errorText }}</span>
  </div>
</template>

<script>
export default {
  name: 'InputField',
  props: {
    label: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    required: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      inputValue: '',
      errorText: 'Поле является обязательным',
      isValid: false,
      isFocus: false,
      hasError: false,
    };
  },
  computed: {
    classes() {
      return {
        'input-field_has-error': this.hasError,
        'input-field_correct': this.isValid,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.input-field {
  width: 100%;

  &__label {
    font-size: 10px;
    line-height: 12px;
    margin-bottom: 4px;
    color: $color-dark-purple;
    letter-spacing: -0.02em;
    display: inline-block;

    &_required {
      position: relative;

      &:before {
        content: '';
        background-color: $color-pink;
        width: 4px;
        height: 4px;
        border-radius: 50%;
        position: absolute;
        top: 0;
        right: -4px;
      }
    }
  }

  &__field {
    font-family: 'Source Sans Pro', sans-serif;
    font-size: 12px;
    line-height: 15px;
    background: $color-primary;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    width: 100%;
    height: 36px;
    outline: none;
    transition: all .3s;
    color: $color-lighten-black;
    border: 1px solid transparent;

    &:focus, &:active {
      border: 1px solid rgba(0, 0, 0, 0.3);
    }

    &::placeholder {
      color: $color-dark-gray;
    }

    &_correct {
      border-color: $color-green;
    }

    &_has-error {
      border-color: $color-pink;
    }
  }
}
</style>
