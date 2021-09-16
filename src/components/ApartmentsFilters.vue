<template>
  <div class="filter">
    <h1>Квартиры в ЖК "Фрукты"</h1>
    <div class="filter-rooms">
      <label class="filter__label">Количество комнат</label>
      <div class="filter-checkboxes">
        <label
          v-for="type in roomTypes"
          :key="type.value"
          class="filter-checkbox-label"
        >
          <input
            v-model="filters.types"
            type="checkbox"
            :value="type.value"
          >
          <span
            class="filter-checkbox-label__checkbox"
            :class="{
              'filter-checkbox-label__checkbox__auto-width': type.autoWidth 
            }"
          >
            {{ type.value }}
          </span>
        </label>
      </div>
    </div>
    <div class="filter-container">
      <div class="filter-container__input-block">
        <label class="filter__label">Стоимость квартиры</label>
        <div class="filter-inputs">
          <div class="filter-inputs__container">
            От <input
              v-model="filters.minCost"
              class="filter-inputs__input"
              placeholder="15 255 999"
              @input="value => filters.minCost = getNumberInputValue(value)"
            >
          </div>
          <div class="filter-inputs__container">
            до <input
              v-model="filters.maxCost"
              class="filter-inputs__input"
              placeholder="155 255 999"
              @input="value => filters.maxCost = getNumberInputValue(value)"
            > ₽
          </div>
        </div>
      </div>
      <div class="filter-container__input-block">
        <label class="filter__label">Общая площадь</label>
        <div class="filter-inputs">
          <div class="filter-inputs__container">
            От <input
              v-model="filters.minSquare"
              class="filter-inputs__input" 
              placeholder="35"
              @input="value => filters.minSquare = getNumberInputValue(value)"
            >
          </div>
          <div class="filter-inputs__container">
            до <input
              v-model="filters.maxSquare"
              class="filter-inputs__input" 
              placeholder="116"
              @input="value => filters.maxSquare = getNumberInputValue(value)"
            > м<sup>2</sup>
          </div>
        </div>
      </div>
    </div>
    <div class="filter-buttons">
      <button
        class="filter-buttons__cancel secondary"
        @click="clearFilters"
      >Сбросить</button>
      <button
        class="filter-buttons__search primary"
        @click="showApartments"
      >Показать 10 квартир</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ApartmentsFilters',
  data() {
    return {
      filters: {
        minCost: '',
        maxCost: '',
        minSquare: '',
        maxSquare: '',
        types: [],
      },
      roomTypes: [
        { value: 'Своб. план.', 'autoWidth': true },
        { value: 'Студия', 'autoWidth': true },
        { value: '1', 'autoWidth': false },
        { value: '2', 'autoWidth': false },
        { value: '3', 'autoWidth': false },
        { value: '4+', 'autoWidth': false },
      ]
    }
  },
  methods: {
    getNumberInputValue(value) {
      return value.target.value
        .replace(/\D/g, '')
        .replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
    clearFilters() {
      this.filters = {
        minCost: '',
        maxCost: '',
        minSquare: '',
        maxSquare: '',
        types: [],
      }
    },
    showApartments() {
      this.$emit('show-apartments', Object.fromEntries(
        Object.entries(this.filters).map(f => {
          if (typeof f[1] === 'string') {
            if (f[1].length === 0) f[1] = '0'
            f[1] = parseInt(f[1].replace(/\D/g, ''))
          }
          return f
        })
      ))
    }
  }
}
</script>

<style scoped lang="scss">
.filter {
  background-color: #fff;
  border: 1px solid #d8d8d8;
  border-radius: 10px;
  padding: 30px;
}
.filter-buttons {
  margin-top: 32px;
  display: flex;
  
  &__search {
    margin-left: auto;
  }
}
.filter-container {
  margin-top: 20px;
  display: flex;
  &__input-block {

    &:not(:last-child) {
      margin-right: 30px;
    }
  }
}
.filter-inputs {
  border: 1px solid #d8d8d8;
  border-radius: 8px;
  padding: 12px;
  display: flex;
  margin-top: 8px;

  &:hover {
    border-color: #79818c;
  }
  &:focus-within {
    border-color: #367ee7;
  }

  &__container {
    flex: 1;
    display: flex;
    color: #79818c;

    &:last-child {
      border-left: 1px solid #d8d8d8;
      padding-left: 8px
    }
    &:first-child {
      padding-right: 8px;
    }
  }

  &__input {
    border: none;
    border-radius: 0;
    outline: none;
    margin: 0 8px;
    padding: 0;
    height: auto;
    width: 100%;
    color: #1f1f25;
    font-size: 16px;

    &::placeholder {
      color: #79818c;
    }
  }
}
.filter-checkboxes {
  margin-top: 8px;
}
.filter-checkbox-label {
  margin-right: 8px;

  input {
    position: absolute;
    z-index: -1;
    opacity: 0;

    &:checked + span {
      background-color: #ffd400;
    }
  }

  &__checkbox {
    border: 1px solid #d8d8d8;
    border-radius: 40px;
    width: 40px;
    height: 40px;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    color: #1f1f25;

    &:hover {
      border-color: #1f1f25;
      cursor: pointer;
    }

    &__auto-width {
      width: auto;
      padding: 0 16px;
    }
  }
}
</style>
