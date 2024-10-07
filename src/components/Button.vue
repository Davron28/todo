<template>
  <button class="open__modal" @click="$emit('openModal')" v-show="!modalOpen">
    <img src="@/assets/img/edit.svg" alt="" />
  </button>
</template>

<script>
export default {
  props: {
    modalOpen: Boolean
  }
};
</script>

<style>
.open__modal {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    linear-gradient(0deg, #fffbfe, #fffbfe);
  box-shadow: 0px 1px 3px 0px #0000004d;
  border-radius: 16px;
  width: 56px;
  height: 56px;
  position: fixed;
  right: 30px;
  bottom: 30px;
  cursor: pointer;
}
</style>