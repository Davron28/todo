<template>
  <div class="notes">
    <div class="container">
      <div class="notes__top">
        <h2 class="notes__title">
          {{ notes.length > 0 ? words.allNotes[lang] : words.notNotes[lang] }}
        </h2>
        <button class="notes__btn" @click="grid = !grid">
          <img v-if="grid" src="@/assets/img/list.svg" alt="" />
          <img v-else src="@/assets/img/grid.svg" alt="" />
          <span>
            {{ grid ? words.list[lang] : words.grid[lang] }}
          </span>
        </button>
      </div>
      <div class="notes__list" :class="{active: !grid}">
        <NoteItem 
        v-for="note in notes" :key="note.id"
        :lang="lang"
        :grid="grid"
        :note="note"
        @delNote="$emit('delNote', note.id)"
        @changeNote="$emit('changeNote', note.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NoteItem from "@/components/NoteItem.vue"
export default {
    components: {
      NoteItem
    },
    data() {
        return {
            grid: true
        }
    },
    props: {
      notes: Array,
      lang: String
    },
    inject: ['words']
};
</script>

<style>
.notes {
  margin: 30px 0;
}
.notes__top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.notes__title {
  font-weight: 400;
  font-size: 22px;
  color: #323232;
}
.notes__btn {
  display: flex;
  align-items: center;
  gap: 12px;
  background: linear-gradient(0deg, #fffbfe, #fffbfe),
    linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11));
  box-shadow: 0px 1px 3px 0px #0000004d;
  border-radius: 16px;
  width: 112px;
  height: 56px;
  justify-content: center;
}
.notes__btn span {
    font-size: 14px;
    color: #6750A4;
    font-family: "rm";
}
.notes__list {
  display: grid;
  margin-top: 30px;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
.notes__list.active {
  grid-template-columns: 1fr;
}
</style>