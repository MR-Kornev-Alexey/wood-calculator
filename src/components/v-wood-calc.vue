<template>
  <v-container>
    <v-row class="d-block">
      <div class="md-6">
        <div>
          Введите объем пиломатериала (доска, брус и т.д) в м3 (в кубометрах)
        </div>
        <v-text-field
          class="result-100 md-6"
          required
          v-model.number="volume"
          type="text"
          @keyup.enter="calcWood()"
          @change="calcWood()"
        />
      </div>
      <div class="md-6">
        <div>Введите толщину пиломатериала в мм</div>
        <v-text-field
          class="result-100 md-6"
          required
          v-model.number="thickness"
          type="text"
          @keyup.enter="calcWood()"
          @change="calcWood()"
        />
      </div>
      <div class="md-6">
        <div>Введите ширину пиломатериала в мм</div>
        <v-text-field
          class="result-100 md-6"
          required
          v-model.number="height"
          type="text"
          @keyup.enter="calcWood()"
          @change="calcWood()"
        />
      </div>
      <div class="md-6">
        <div>Введите длину пиломатериала в м</div>
        <v-text-field
          class="result-100 md-6"
          required
          v-model.number="length"
          type="text"
          @keyup.enter="calcWood()"
          @change="calcWood()"
        />
      </div>
    </v-row>
    <v-row>
      <v-col>
        <h2>Результат перевода:</h2>
        <div v-if="flagRender">{{ outCalc }} штук</div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "v-wood-calc",
  methods: {
    calcWood() {
      this.flagRender = false;
      if (
        this.volume > 0 &&
        this.thickness > 0 &&
        this.height > 0 &&
        this.length > 0
      ) {
        this.outCalc = Math.floor(
          this.volume /
            (this.thickness * this.height * this.length * 0.001 * 0.001)
        );
        this.flagRender = true;
      }
      return false;
    }
  },
  data: () => ({
    flagRender: false,
    volume: "",
    outCalc: "",
    thickness: "",
    height: "",
    length: ""
  })
};
</script>
<style>
.result-100 {
  width: 200px;
}
</style>
