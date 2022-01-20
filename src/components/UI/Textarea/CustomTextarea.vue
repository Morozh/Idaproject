<template>
  <div class="textarea-field">
    <label class="textarea-field__label">{{ label }}</label>
    <textarea
      class="textarea-field__field"
      type="text"
      :value="modelValue"
      :placeholder="placeholder"
      :class="classes"
      @input="updateValue($event.target.value)"
    />
    <span class="textarea-field__msg" v-show="hasError">{{ errorText }}</span>
  </div>
</template>

<script>
export default {
  name: 'TextareaField',
  props: {
    label: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    modelValue: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      textareaValue: '',
      errorText: '',
      isFocus: false,
      hasError: false,
    };
  },
  computed: {
    classes() {
      return {
        'textarea-field_has-error': this.hasError,
        'textarea-field_focused': this.isFocus,
      };
    },
  },
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value);
    },
  },
};
</script>

<style lang="scss" scoped>
.textarea-field {
  display: flex;
  flex-direction: column;

  &__label {
    font-size: 10px;
    line-height: 12px;
    margin-bottom: 4px;
    color: $color-dark-purple;
    letter-spacing: -0.02em;
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
    min-height: 108px;
    outline: none;
    transition: all .3s;
    color: $color-lighten-black;
    border: 1px solid transparent;
    resize: none;

    &:focus, &:active {
      border: 1px solid rgba(0, 0, 0, 0.3);
    }

    &::placeholder {
      color: $color-dark-gray;
    }

    &::-webkit-scrollbar {
      width: 2px;
      border-radius: 100%;
    }

    &::-webkit-scrollbar-track {
      box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
    }

    &::-webkit-scrollbar-thumb {
      background-color: darkgrey;
      outline: 1px solid slategrey;
    }
  }
}
</style>
