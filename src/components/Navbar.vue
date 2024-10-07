<template>
  <header class="header">
    <Transition name="header__notes">
      <nav class="header__notes" v-show="header === true">
        <button class="header__lang" @click="changeLang">
          {{ lang == "ru" ? 'RU' : 'UZ' }}
        </button>
        <h1 class="header__title"> {{ words.notes[lang] }} </h1>
        <button class="header__search" @click="header = false">
          <img src="@/assets/img/search.svg" alt="" />
        </button>
      </nav>
    </Transition>
    <Transition name="header__form">
        <nav class="header__form" v-show="header === false">
          <button class="header__back" @click="header = true">
            <img src="@/assets/img/back.svg" alt="" />
          </button>
          <input
            type="text"
            class="header__input"
            :placeholder="words.search[lang]"
            v-model="search"
          />
          <button class="header__close" @click="search = ''">
            <img src="@/assets/img/close.svg" alt="" />
          </button>
        </nav>
    </Transition>
  </header>
</template>

<script>
export default {
  data() {
    return {
      header: true,
      search: "",
    };
  },
  watch: {
    search(val) {
      this.$emit('searchValue', val)
    }
  },
  props: ["lang"],
  methods: {
    changeLang() {
      this.$emit('changeLang', this.lang == "ru" ? "uz" : "ru")
    }
  },
  inject: ['words']
};
</script>

<style>
.header {
  height: 70px;
  background: #f3edf7;
  box-shadow: 0px 4px 4px 0px #00000040;
  padding: 18px 20px;
  overflow: hidden;
}

.header__notes,
.header__form {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

button {
  border: none;
  background: transparent;
  cursor: pointer;
}

.header__lang {
  font-size: 23px;
  font-family: "rm";
  font-weight: bold;
}

.header__title {
  color: #1c1b1f;
  font-size: 22px;
  font-weight: 400;
}

.header__input {
  width: 80%;
  background: transparent;
  border: none;
  outline: none;
  font-size: 16px;
  color: #9d9d9d;
}

/* Header notes */

.header__notes-enter-active, 
.header__notes-leave-active {
    transition: 1000ms linear;
}
.header__notes-enter-from,
.header__notes-leave-to {
    opacity: 0;
    transform: translateY(-200px);
}
.header__notes-enter-to,
.header__notes-leave-from {
    opacity: 1;
    transform: translateY(0px);
}

/* Header form */

.header__form-enter-active, 
.header__form-leave-active {
    transition: 1000ms linear;
}
.header__form-enter-from,
.header__form-leave-to {
    opacity: 0;
    transform: translateY(200px);
}
.header__form-enter-to,
.header__form-leave-from {
    opacity: 1;
    transform: translateY(0px);
}

</style>