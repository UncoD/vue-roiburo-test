<template>
  <div class="apartments-catalog">
    <ApartmentsFilters
      @show-apartments="showApartments"
    />
    <div
      v-if="apartments && apartments.length > 0"
      class="results"
    >
      <h2>Найдено {{ apartments.length }} квартир</h2>
      <table class="results__table" width="100%">
        <tr>
          <th
            v-for="field in fields"
            :key="field.key"
          >{{ field.label }}</th>
        </tr>
        <template v-for="(apartment, i) in apartments">
          <tr
            :class="{ opened: opened.includes(i) }"
            :key="i"
            class="results__body-row"
          >
            <td
              v-for="(field, j) in fields"
              :key="j"
              @click="toggle(i)"
              :class="{
                'results__body-row__bold': field.bold
              }"
            >
              <template v-if="field.key === 'type'">
                {{ getFormatType(apartment[field.key]) }}
              </template>
              <template v-else-if="field.key === 'square'">
                {{ apartment[field.key] }} м<sup>2</sup>
              </template>
              <template v-else-if="field.key === 'price'">
                {{ getFormatPrice(apartment[field.key]) }} ₽
              </template>
              <template v-else>
                {{ apartment[field.key] }}
              </template>
            </td>
            <td class="results__row-btn heart-btn">
              <button class="results__heart-btn secondary"></button>
            </td>
            <td
              class="results__row-btn arrow-btn"
              @click="toggle(i)"
            >
              <div
                class="results__expand-btn"
                :class="{
                  'results__expand-btn__inverted': opened.includes(i)
                }"
              />
            </td>
          </tr>
          <tr
            v-if="opened.includes(i)"
            :key="i + '_expanded'"
            class="results__body-row__expanded"
          >
            <td :colspan="fields.length + 2">
              <ApartmentInfo :apartment="apartment"/>
            </td>
          </tr>
        </template>
        <tr>
        </tr>
      </table>
    </div>
    <div
      v-else
      class="not-found"
    >
      <img src="@/assets/images/not_found.svg">
      <div class="not-found__text">
        <h2>Мы ничего похожего не нашли</h2>
        <p>Попробуйте задать другие условия поиска или сбросьте фильтр</p>
      </div>
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
      fields: [
        { key: 'type', label: 'Тип', bold: true },
        { key: 'floor', label: 'Этаж', bold: false },
        { key: 'deadline', label: 'Срок сдачи', bold: false },
        { key: 'square', label: 'Площадь', bold: false },
        { key: 'price', label: 'Стоимость', bold: true },
      ],
      opened: [],
      apartments: []
    }
  },
  methods: {
    showApartments(values) {
      this.apartments = values
    },
    toggle(id) {
      const index = this.opened.indexOf(id);
      if (index > -1) {
        this.opened.splice(index, 1)
      } else {
        this.opened.push(id)
      }
    },
    getFormatType(type) {
      if (Number.isInteger(parseInt(type))) {
        return type + '-комн.'
      }
      return type
    },
    getFormatPrice(price) {
      return (price + '').replace(/\B(?=(\d{3})+(?!\d))/g, ' ')
    }
  }
}
</script>

<style scoped lang="scss">
.results, .not-found {
  background-color: #fff;
  border: 1px solid #d8d8d8;
  border-radius: 10px;
  padding: 30px 0;
  margin-top: 32px;
  overflow: hidden;
}
.results {
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
    background: #f1f5f9 url("../assets/images/heart.svg") no-repeat 50% 50%;
    border-radius: 40px;
    width: 40px;
    height: 40px;
    padding: 0;
  }

  &__expand-btn {
    user-select: none;
    background: url("../assets/images/down.svg") no-repeat 50% 50%;
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

.not-found {
  display: flex;
  align-items: center;
  padding: 30px 60px 30px 30px;

  img {
    margin-right: 52px;
    width: 240px;
    height: 240px;
  }

  h2 {
    margin-bottom: 12px;
  }

  p {
    margin: 0;
  }
}
</style>
