<template>
  <div class="status-bar">
    <div>
      <label for="scale">Масштаб</label>
      <input
        type="range"
        class="scale"
        id="scale"
        name="scale"
        min="12"
        max="300"
        step="1"
        :value="scale"
        @input="updateScale"
      />
    </div>
    <div v-if="imgLoaded && imageWidth !== null && imageHeight !== null && imageWidth !== 300 && imageHeight !== 150"> <!-- Изменено условие отображения -->
      Ширина: {{ imageWidth }} Высота: {{ imageHeight }}
    </div>
    <div v-if="state === 'pipette' && pickedColor">
      Цвет: {{ pickedColor }}
    </div>
    <div
      v-if="state === 'pipette' && pickedColor"
      class="pipette-color"
      :style="{
        background: pickedColor,
      }"
    ></div>
    <div v-if="state === 'pipette' && pickedColor && xMouse !== null && yMouse !== null">
      Координаты: {{ xMouse }}:{{ yMouse }}
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "StatusBar",
  props: {
    state: String,
    imageHeight: Number,
    imageWidth: Number,
    pickedColor: String,
    xMouse: Number,
    yMouse: Number,
    scale: Number,
    imgLoaded: Boolean, // Добавили этот параметр
  },
  methods: {
    updateScale(event) {
      const newScale = +event.target.value;
      this.$emit("updateScale", newScale);
    },
  },
});
</script>

<style scoped lang="scss">
.status-bar {
  position: absolute;
  bottom: 0;
  width: calc(100% - 60px);
  height: 20px;
  background: linear-gradient(to right, #61ccbf, #ececec,);
  display: flex;
  gap: 5px;
  justify-content: space-between;
  padding-bottom: 5px;
}

.left-side {
  display: flex;
}

.pipette-color {
  margin-top: 2.5px;
  width: 15px;
  height: 15px;
}

.scale {
  margin-right: 13px;
}
</style>
