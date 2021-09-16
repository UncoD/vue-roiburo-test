<template>
  <div class="apartments-catalog">
    <ApartmentsFilters
      @show-apartments="showApartments"
    />
    <div class="results">
      <h2>Найдено 10 квартир</h2>
      <table class="results__table" width="100%">
        <tr>
          <th
            v-for="field in fields"
            :key="field.key"
          >{{ field.label }}</th>
        </tr>
        <template v-for="(row) in 3">
          <tr
            :class="{ opened: opened.includes(row) }"
            :key="row"
            class="results__body-row"
          >
            <td
              v-for="i in fields.length"
              :key="i"
              :class="{
                'results__body-row__bold': fields[i - 1].bold
              }"
              @click="toggle(row)"
            >Ячейка {{ i }}</td>
            <td class="results__row-btn heart-btn">
              <button class="results__heart-btn secondary"></button>
            </td>
            <td
              class="results__row-btn arrow-btn"
              @click="toggle(row)"
            >
              <div
                class="results__expand-btn"
                :class="{
                  'results__expand-btn__inverted': opened.includes(row)
                }"
              />
            </td>
          </tr>
          <tr
            v-if="opened.includes(row)"
            :key="row * 5"
            class="results__body-row__expanded"
          >
            <td :colspan="fields.length + 2">
              <ApartmentInfo />
            </td>
          </tr>
        </template>
        <tr>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import ApartmentsFilters from './ApartmentsFilters.vue'
import ApartmentInfo from './ApartmentInfo.vue'
export default {
  name: 'ApartmentsCatalog',
  components: {
    ApartmentsFilters,
    ApartmentInfo
  },
  data() {
    return {
      filters: {},
      fields: [
        { key: 'type', label: 'Тип', bold: true },
        { key: 'floor', label: 'Этаж', bold: false },
        { key: 'deadline', label: 'Срок сдачи', bold: false },
        { key: 'square', label: 'Площадь', bold: false },
        { key: 'cost', label: 'Стоимость', bold: true },
      ],
      opened: [],
    }
  },
  methods: {
    showApartments(values) {
      this.filters = values
    },
    toggle(id) {
      const index = this.opened.indexOf(id);
      if (index > -1) {
        this.opened.splice(index, 1)
      } else {
        this.opened.push(id)
      }
    }
  }
}
</script>

<style scoped lang="scss">
.results {
  background-color: #fff;
  border: 1px solid #d8d8d8;
  border-radius: 10px;
  padding: 30px 0;
  margin-top: 32px;
  overflow: hidden;

  h2 {
    padding: 0 30px;
  }

  &__table {
    border-collapse: collapse;
    th {
      text-align: left;
      font-size: 14px;
      font-weight: 400;
      height: 48px;
      padding-left: 30px;
    }
  }

  &__body-row {
    &__bold {
      font-weight: 700;
    }
    &__expanded {
      td {
        padding: 30px 30px;
        box-shadow: 0px 10px 10px 0px #0000001f;
      }
      & + .results__body-row td::after {
        height: 0;
      }
    }
    td {
      position: relative;
      height: 72px;
      padding-left: 30px;
      
      &::after {
        content: "";
        background: #f1f5f9;
        position: absolute;
        top: 0px;
        left: 0px;
        height: 1px;
        width: 100%;
      }
      &:first-child,
      &:last-child {
        &::after {
          left: 30px;
          width: calc(100% - 30px);
        }
      }
      &:last-child::after {
        left: 0px;
      }
    }
    &:hover {
      box-shadow: 0px 5px 15px 0px #0000001f;
      cursor: pointer;
      td::after,
      & + .results__body-row td::after {
        height: 0;
      }
    }
  }

  &__heart-btn {
    background: #f1f5f9 url("../assets/heart.svg") no-repeat 50% 50%;
    border-radius: 40px;
    width: 40px;
    height: 40px;
    padding: 0;
  }

  &__expand-btn {
    user-select: none;
    background: url("../assets/down.svg") no-repeat 50% 50%;
    width: 20px;
    height: 20px;
    &__inverted {
      transform: scale(1, -1);
    }
  }

  &__row-btn {
    &.heart-btn {
      width: 40px;
      padding-left: 0;
    }
    &.arrow-btn {
      width: 20px;
      padding: 0 30px 0 20px;
    }
  }
}
</style>
