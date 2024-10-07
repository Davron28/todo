<template>
    <Transition name="modal">
        <div class="modal" @click="closeModal">
          <div class="modal__content" @click.stop="">
              <h2 class="modal__content-title">
                {{ edit ? words.editModal[lang] : words.addModal[lang] }}
              </h2>
              <div class="modal__inputs">
                  <label>
                      <span>Title</span>
                      <input type="text" placeholder="Title" v-model="title">
                  </label>
                  <label>
                      <span>Content</span>
                      <textarea placeholder="Content" v-model="descr"></textarea>
                  </label>
              </div>
              <div class="modal__btns">
                  <button class="modal__btn return" @click="closeModal">{{words.cancel[lang]}}</button>
                  <button v-if="!edit" class="modal__btn add" @click="addNote">{{words.add[lang]}}</button>
                  <button v-else class="modal__btn add" @click="changeNote">{{words.change[lang]}}</button>
              </div>
          </div>
        </div>
    </Transition>
</template>

<script>
export default {
 data() {
    return {
        title: "",
        descr: "",
        id: this.currentId
    }
 },
 methods: {
    closeModal() {
        this.$emit("closeModal", false)
        this.title = '';
        this.descr = '';
    },
    addNote() {
        if(this.title != '' && this.descr != '') {
            const item = {
                id: this.id++,
                title: this.title,
                descr: this.descr,
                date: new Date().toLocaleDateString(),
            }
            this.$emit('addNote', item)
            this.title = '';
            this.descr = '';
        }
    },
    changeNote() {
        if(this.title != '' && this.descr != '') {
            const editedNote = {
                id: this.editNote.id,
                title: this.title,
                descr: this.descr,
                date: new Date().toLocaleDateString(),
            }
            this.$emit('editedNote', editedNote);
            this.closeModal();
        }
    }
 },
 props: {
    currentId: Number,
    edit: Boolean,
    editNote: Object,
    lang: String
 },
 inject: ['words']
}
</script>

<style>

.modal {
    display: flex;
    align-items: center;
    justify-content: center;
    background: #00000059;
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
}

.modal__content {
    width: 312px;
    background: linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11)),
        linear-gradient(0deg, #FFFBFE, #FFFBFE);
    border-radius: 28px;
    padding: 24px;
}

.modal__content-title {
    font-family: rm;
    font-weight: 400;
    font-size: 24px;
    line-height: 32px;
    color: #1C1B1F;
    margin-bottom: 16px;
}

.modal__inputs {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    gap: 16px;
}

.modal__inputs label {
    position: relative;
    user-select: none;
}

.modal__inputs input {
    height: 56px;
    width: 100%;
    outline: none;
    border: none;
    background: #E7E0EC;
    border-radius: 4px 4px 0 0;
    border-bottom: 1px solid #1C1B1F;
    font-weight: 400;
    font-size: 16px;
    letter-spacing: 0.5s;
    line-height: 24px;
    color: #49454F;
    padding: 8px 0 0 16px;
}

.modal__inputs span {
    position: absolute;
    top: 8px;
    left: 16px;
    font-size: 12px;
    letter-spacing: 0.4px;
    line-height: 16px;
    color: #6750A4;
}

.modal__inputs textarea {
    height: 56px;
    width: 100%;
    outline: none;
    border: none;
    background: #E7E0EC;
    border-radius: 4px 4px 0 0;
    border-bottom: 1px solid #1C1B1F;
    font-weight: 400;
    font-size: 16px;
    letter-spacing: 0.5s;
    line-height: 24px;
    color: #49454F;
    padding: 23px 0 0 16px;
    resize: none;
}

.modal__btns {
    display: flex;
    justify-content: flex-end;
    width: 100%;
    gap: 6px;
    margin-top: 24px;
}

.modal__btn {
    padding: 10px 12px 10px 12px;
    font-family: "rm";
    font-size: 14px;
    line-height: 20px;
    transition-duration: .3s;
    text-transform: uppercase;
}

.return{
    color: #CF1B1B;
}

.add{
    color: #6750A4;
}

.return:hover {
    background: #FFE1E1;
}

.add:hover{
    background: #E6DDFF;
}

.modal-enter-active, 
.modal-leave-active {
    transition: 300ms linear;
}
.modal-enter-from,
.modal-leave-to {
    opacity: 0;
    transform: scale(1.5);
}

</style>