<template>
  <Transition name="notes__item">
    <div class="notes__item">
      <div class="notes__item-top" :class="{between: !grid}">
        <h2 class="notes__item-title">{{ note.title }}</h2>
        <p class="notes__item-date">{{ note.date }}</p>
      </div>
      <p class="notes__item-descr">
        {{ note.descr }}
      </p>
      <div class="notes__item-btns">
        <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
          <img src="@/assets/img/edit.svg" alt="" />
          <span> {{ words.editNotes[lang] }} </span>
        </button>
        <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
          <img src="@/assets/img/del.svg" alt="" />
          <span> {{ words.delNotes[lang] }} </span>
        </button>
      </div>
    </div>
  </Transition>
</template>

<script>
import { inject } from 'vue';
export default {
    props: {
        grid: Boolean,
        note: Object,
        lang: String
    },
    inject: ['words']
};
</script>

<style>
.notes__item {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.05),
      rgba(103, 80, 164, 0.05)
    ),
    linear-gradient(0deg, #fffbfe, #fffbfe);
  box-shadow: 0px 1px 3px 1px #00000026;
  padding: 16px;
  border-radius: 16px;
}
.notes__item-title {
    color: #1C1B1F;
    font-size: 16px;
    font-family: "rm";
    font-weight: 500;
    line-height: 24px;
}
.notes__item-date {
    font-size: 14px;
    letter-spacing: 0.25px;
    color: #CAC4D0;
    line-height: 20px;
}
.notes__item-top {
    margin-bottom: 16px;
}
.notes__item-top.between {
    display: flex;
    justify-content: space-between;
}
.notes__item-descr {
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.25px;
    color: #49454F;
    margin-bottom: 17px;
}
.notes__item-btns {
    display: flex;
    justify-content: flex-end;
    align-items: center;
}
.notes__item-btn {
    padding: 12px;
    display: flex;
    gap: 8px;
    align-items: center;
    transition: 300ms;
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.1px;
    font-family: "rm";
}
.del {
    color: #CF1B1B;
}
.del:hover {
    background: #FFE1E1;
}
.edit {
    color: #6750A4;
}
.edit:hover {
    background: #E6DDFF;
}
/* .notes__item-enter-active, 
.notes__item-leave-active {
    transition: 300ms linear;
}
.notes__item-enter-from,
.notes__item-leave-to {
    opacity: 0;
    transform: scale(1.5);
} */
</style>