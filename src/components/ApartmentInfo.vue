<template>
  <div class="apartment-info">
    <div class="labels">
      <span class="labels__label labels__label__green">Скидка 2%</span>
      <span class="labels__label labels__label__orange">Материнский капитал</span>
      <span class="labels__label labels__label__purple">Ипотека от 0,1%</span>
    </div>
    <div class="description">
      <img
        class="description__image"
        :src="image"
      >
      <div class="description-text">
        <h2>2—комнатная квартира</h2>
        <div class="description-text__params">
          <div class="description-text__param">22 356 000 ₽</div>
          <div class="description-text__param">155 м<sup>2</sup></div>
        </div>
        <div class="description-info">
          <div class="description-info-block">
            <label>Цена за м<sup>2</sup></label>
            <span>120 000 ₽</span>
          </div>
          <div class="description-info-block">
            <label>Отделка</label>
            <span>Без отделки</span>
          </div>
          <div class="description-info-block">
            <label>Корпус</label>
            <span>3</span>
          </div>
        </div>
        <a href="#" class="description-text__more-info">Подробное описание</a>
      </div>
    </div>
    <div class="sign-up">
      <h3>Хотите записаться на просмотр объекта?</h3>
      <p>Оставьте свои данные, и мы организуем просмотр в удобное для вас время.</p>
      <form
        class="sign-up-form"
      >
        <div class="sign-up-form__block">
          <label for="name">Имя</label>
          <input
            type="text"
            name="name"
            placeholder="Введите имя"
          >
        </div>
        <div class="sign-up-form__block">
          <label for="phone">Номер телефона</label>
          <input
            name="phone"
            placeholder="+7"
          >
        </div>
        <button
          type="button"
          class="sign-up-form__btn primary"
        >Оставить заявку</button>
      </form>
      <p class="sign-up__confidentiality">
        Оставляя заявку вы соглашаетесь с <a href="#">политикой конфидециальности</a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ApartmentsInfo',
  props: {
    img: { type: String, default: "apartment.png"},
  },
  data() {
    return {
    }
  },
  computed: {
    image() {
      return require('../assets/' + this.img)
    }
  },
  methods: {
  }
}
</script>

<style scoped lang="scss">
.labels {
  &__label {
    border-radius: 50px;
    padding: 5px 10px;
    margin-right: 8px;
    font-weight: 500;
    font-size: 14px;

    &__green {
      color: #56B77f;
      padding-right: 32px;
      background: #ddffe2 url("../assets/green_question.svg") calc(100% - 10px) no-repeat;
    }

    &__orange {
      color: #f2994a;
      padding-right: 32px;
      background: #fff7f2 url("../assets/orange_question.svg") calc(100% - 10px) no-repeat;
    }

    &__purple {
      background: #e1e0fc;
      color: #9796d0;
    }
  }
}
.description {
  display: flex;
  align-items: center;
  padding: 20px 0;

  &__image {
    width: 215px;
    height: 215px;
    object-fit: contain;
    margin-right: 12px;
  }
}
.description-text {
  flex: 1;

  h2 {
    margin-bottom: 16px;
  }

  &__more-info {
    text-decoration: none;
    font-weight: 700;
    position: relative;
    &::after {
      content: "";
      background: url("../assets/right.svg") no-repeat;
      position: absolute;
      top: 0;
      right: -20px;
      width: 16px;
      height: 16px;
    }
  }

  &__params {
    display: flex;
    align-items: flex-end;
    font-size: 14px;
  }

  &__param:first-child {
    border-right: 1px solid #d8d8d8;
    padding-right: 16px;
  }
  &__param:last-child {
    padding-left: 16px;
  }
}
.description-info {
  display: flex;
  margin: 17px 0 15px;
}
.description-info-block {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}
.sign-up {
  border-top: 1px solid #d8d8d8;
  padding-top: 20px;

  &__confidentiality {
    color: #79818c;
  }
}
.sign-up-form {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  align-items: flex-end;

  &__block {
    display: flex;
    flex-direction: column;
  }

  &__btn {
    height: 50px;
    padding: 0 10px;
  }
}
</style>
