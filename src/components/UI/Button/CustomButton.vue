<template>
  <button
    class="custom-button"
    :class="{ 'custom-button_active': !disabled }"
    :disabled="disabled"
    @click="handleClick"
  >
    <slot name="text"></slot>
  </button>
</template>

<script>
export default {
  name: 'CustomButton',
  props: {
    disabled: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {};
  },
  methods: {
    handleClick(e) {
      this.$emit('cb', e.target);
    },
  },
};
</script>

<style lang="scss" scoped>
.custom-button {
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 12px;
  line-height: 14px;
  font-weight: 600;
  padding: 10px;
  transition: all .3s;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: $color-gray;
  color: $color-dark-gray;
  border: none;
  border-radius: 10px;

  &_active {
    color: $color-white;
    background-color: $color-green;
    cursor: pointer;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);

    &:hover {
      transform: scale(1.01);
    }
  }
}
</style>
