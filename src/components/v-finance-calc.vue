<template>
  <v-container>
    <v-row class="d-flex">
      <div class="md-5 block-grey">
        <div>
          <h2>Выберите условия</h2>
        </div>
        <v-flex class="my-4">
          <label>
            <select @click="getType()" v-model="selected">
              <option disabled value="">Выберите один из вариантов</option>
              <option value="acquiring">займ под эквайринг</option>
              <option value="on-line-shop">займ для интернет-магазинов</option>
            </select>
          </label>
        </v-flex>
        <div class="my-4">
          <h3>
            Введите сумму займа
          </h3>

          <span class="grey--text">от 100 000 до 1 000 000 рублей</span>
        </div>
        <div>
          <label>
            <input
              @change="inputRate()"
              @keypress.enter="inputRate()"
              class="input-number "
              type="number"
              v-model="value"
            />
          </label>
          рублей
        </div>
        <div class="wrapper d-block">
          <label>
            <input
              @change="inputRate()"
              class="my-5"
              max="1000000"
              min="100000"
              step="1"
              type="range"
              v-model="value"
            />
          </label>
        </div>
        <div class="my-4">
          <h3>
            Введите срок займа
          </h3>

          <span class="grey--text">от 15 до 90 дней</span>
        </div>
        <div>
          <button
            :class="[
              { 'btn-items-section_selected': item.selected },
              { 'btn-items-section': !item.selected }
            ]"
            :key="item.id"
            @click="changeDaySelection(item.id)"
            v-for="item in days"
          >
            {{ item.name }}
          </button>
        </div>
      </div>
      <div class="md-2 block-grey ">
        <div>
          <h2>Наши предложения</h2>
        </div>
        <div class="my-4">
          <div style="height: 40px">
            <h3>
              Ежедневный платеж
            </h3>
          </div>

          <div v-show="flagRender" class="out-data">{{ rateCalc }} рублей</div>
        </div>
        <div class="my-4">
          <div style="height: 40px">
            <h3>
              Процентная ставка
            </h3>
          </div>
          <div v-show="flagRender" class="out-data">
            {{ statePercent }} процентов
          </div>
        </div>
      </div>
      <div class="md-5"></div>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "v-finance-calc",
  methods: {
    getType() {
      this.flagTypeSelection = this.selected;
      if (this.selected === "acquiring") {
        this.statePercent = 3.6;
      } else {
        this.select = {
          report: "займ для интернет-магазинов",
          src: "on-line-shop"
        };
        this.statePercent = this.days[this.stateId].rate;
        this.stateTender = this.days[this.stateId].tender;
      }
      this.calculating();
    },
    calculating() {
      this.flagRender = false;
      let amount = Number(this.value);
      let percent = Number(this.statePercent);
      let days = Number(this.flagDaySelection);
      if (this.flagTypeSelection === "acquiring") {
        this.rateCalc = (
          (amount + amount * (percent / 100) * days) /
          days
        ).toFixed(2);
      } else {
        let tender = Number(this.stateTender);
        this.rateCalc = (
          (amount + (amount * tender) / 100 + amount * (percent / 100) * days) /
          days
        ).toFixed(2);
      }
      this.flagRender = true;
    },
    inputRate() {
      this.calculating();
    },
    changeDaySelection(id) {
      let index = 0;
      while (index < this.days.length) {
        if (index === id) {
          this.days[id].selected = true;
          this.flagDaySelection = this.days[id].days;
          this.stateId = id;
        } else {
          this.days[index].selected = false;
        }
        index++;
      }
      this.calculating();
    }
  },
  data: () => ({
    selected: "",
    items: [
      {
        report: "займ под эквайринг",
        src: "acquiring"
      },
      {
        report: "займ для интернет-магазинов",
        src: "on-line-shop"
      }
    ],
    value: 100000,
    flagDaySelection: 15,
    statePercent: 3.6,
    stateId: 0,
    flagTypeSelection: "acquiring",
    stateTender: 1.6,
    days: [
      {
        id: 0,
        selected: true,
        name: "15 дней",
        days: 15,
        rate: 1.6,
        tender: 1.6
      },
      {
        id: 1,
        selected: false,
        name: "30 дней",
        days: 30,
        rate: 2.5,
        tender: 2.5
      },
      {
        id: 2,
        selected: false,
        name: "45 дней",
        days: 45,
        rate: 2.7,
        tender: 1.6
      },
      {
        id: 3,
        selected: false,
        name: "60 дней",
        days: 65,
        rate: 3,
        tender: 1.6
      },
      {
        id: 4,
        selected: false,
        name: "90 дней",
        days: 90,
        rate: 5,
        tender: 1.6
      }
    ],
    flagRender: false,
    rateCalc: 0,
    percentCalc: 0
  })
};
</script>
<style lang="scss">
.out-data {
  color: darkred;
  height: 40px;
}
.block-grey {
  background-color: #dedede;
  padding: 40px;
  margin: 0 10px;
}

/*для ползунка */
input[type="range"] {
  -webkit-appearance: none; /* Скрывает слайдер, чтобы можно было создать свой */
  width: 100%; /* Указание параметра ширины требуется для Firefox. */
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
}

input[type="range"]:focus {
  outline: none; /* Убирает голубую границу у элемента. Хотя, возможно, и стоит создавать некоторое оформления для состояния фокуса в целях обеспечения доступности. */
}

input[type="range"]::-ms-track {
  width: 100%;
  cursor: pointer;
  background: transparent; /* Скрывает слайдер, чтобы можно было добавить собственные стили. */
  border-color: transparent;
  color: transparent;
}

/* Специальные правила для браузеров на движках WebKit/Blink */
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
  margin-top: -14px; /* Вам нужно указать значение для поля в Chrome, но в Firefox и IE это происходит автоматически */
  box-shadow: 1px 1px 1px #13351c, 0px 0px 1px #14361d;
  border: 1px solid #4b1b85;
}

/* Тоже самое для Firefox */
input[type="range"]::-moz-range-thumb {
  box-shadow: 1px 1px 1px #13351c, 0px 0px 1px #14361d;
  border: 1px solid #4b1b85;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
}

/* Тоже самое для IE */
input[type="range"]::-ms-thumb {
  box-shadow: 1px 1px 1px #13351c, 0px 0px 1px #14361d;
  border: 1px solid #4b1b85;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
}

input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  background: #4b1b85;
  border-radius: 1.3px;
  border: 0.2px solid #010101;
}

input[type="range"]:focus::-webkit-slider-runnable-track {
  background: #4b1b85;
}

input[type="range"]::-moz-range-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  background: #4b1b85;
  border-radius: 1.3px;
  border: 0.2px solid #010101;
}

input[type="range"]::-ms-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  background: transparent;
  border-color: transparent;
  border-width: 16px 0;
  color: transparent;
}

input[type="range"]::-ms-fill-lower {
  background: #4b1b85;
  border: 0.2px solid #010101;
  border-radius: 2.6px;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}

input[type="range"]:focus::-ms-fill-lower {
  background: #4b1b85;
}

input[type="range"]::-ms-fill-upper {
  background: #4b1b85;
  border: 0.2px solid #010101;
  border-radius: 2.6px;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}

input[type="range"]:focus::-ms-fill-upper {
  background: #4b1b85;
}
.btn-items-section:hover {
  background-color: #4b1b85;
  color: white;
}
.btn-items-section {
  background-color: white;
  font-size: 12px;
  color: #4b1b85;
  padding: 4px;
  width: 100px;
  text-transform: uppercase;
  border: 2px solid #4b1b85;
  border-radius: 5px;
  margin: 6px 3px;
}

.btn-items-section_selected {
  background-color: #4b1b85;
  font-size: 12px;
  color: white;
  padding: 6px;
  width: 100px;
  text-transform: uppercase;
  border-radius: 5px;
  margin: 6px 3px;
}
</style>
