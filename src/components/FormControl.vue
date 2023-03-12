<template>
  <form class="card card-w30">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="selectedType">
        <option
          v-for="type in blockType"
          :value="type.value"
          :key="type"
        >
          {{ type.text }}
        </option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea
        id="value"
        rows="3"
        v-model.trim="text"
      />
    </div>
    <button
      class="btn primary"
      :disabled="disabledBtn"
      @click="createResumeField"
    >
      Добавить
    </button>
  </form>
</template>

<script>
export default {
  data () {
    return {
      blockType: [
        {
          value: 'title',
          text: 'Заголовок'
        },
        {
          value: 'subtitle',
          text: 'Подзаголовок'
        },
        {
          value: 'avatar',
          text: 'Аватар'
        },
        {
          value: 'text',
          text: 'Текст'
        }
      ],
      selectedType: 'title',
      text: ''
    }
  },
  methods: {
    createResumeField () {
      this.$emit('getResumeField', {
        type: this.selectedType,
        text: this.text
      })
      this.selectedType = 'title'
      this.text = ''
    }
  },
  computed: {
    disabledBtn () {
      return this.text.length <= 3
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
