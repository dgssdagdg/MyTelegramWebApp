<template>
  <div class="slider-container">
      <button @click="decrement">-</button>
      <div class="slider" @mousedown="startDrag" @touchstart="startDrag" @click="setValue">
          <div class="slider-track"></div>
          <div
              class="slider-thumb"
              :style="thumbStyle"
              ref="thumb"
              @mousedown="startDrag"
              @touchstart="startDrag"
              @mouseover="showValue"
              @mouseleave="hideValue"
          ></div>
          <div class="slider-fill" :style="fillStyle"></div>
          <p v-if="valueVisible" class="value-display" :style="valueDisplayStyle">{{ totalColons }}</p>
      </div>
      <button @click="increment">+</button>
  </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
export default {
  data() {
    return {
      maxValue: 8,
      isDragging: false,
      sliderWidth: 300, // ширина ползунка
      valueVisible: false, // переменная для контроля видимости значения
    };
  },
  computed: {
    ...mapState({
        totalColons: state => state.home.totalColons,
    }),
    thumbStyle() {
      const percentage = (this.totalColons / this.maxValue) * 100;
      return {
        left: `calc(${percentage}% - 10px)`, // -10px, чтобы центрировать круг
      };
    },
    fillStyle() {
      const percentage = (this.totalColons / this.maxValue) * 100;
      return {
        width: `${percentage}%`,
      };
    },
    valueDisplayStyle() {
        const percentage = (this.totalColons / this.maxValue) * 100;
        return {
          left: `calc(${percentage}% - 12px)`, // Центрируем значение над кружком
        top: '-40px', // Отодвигаем значение вверх
        position: 'absolute', // Фиксируем значение на экране
      };
    },
  },
  methods: {
      ...mapMutations({
        SetTotalColons: 'SetTotalColons',
      }),
      increment() {
          if (this.totalColons < this.maxValue) {
              this.SetTotalColons(this.totalColons += 1)
          }
      },
      decrement() {
          if (this.totalColons > 0) {
            this.SetTotalColons(this.totalColons -= 1)
          }
      },
      startDrag(event) {
          this.isDragging = true;
          document.addEventListener('mousemove', this.onDrag);
          document.addEventListener('mouseup', this.stopDrag);
          document.addEventListener('touchmove', this.onDrag);
          document.addEventListener('touchend', this.stopDrag);
      },
      onDrag(event) {
          const sliderRect = this.$el.querySelector('.slider').getBoundingClientRect();
          const offsetX = event.clientX - sliderRect.left; // Получаем x-координату относительно ползунка
          let newValue = Math.round((offsetX / this.sliderWidth) * this.maxValue);
          // Ограничиваем значение между 0 и maxValue
          newValue = Math.max(0, Math.min(newValue, this.maxValue));
          this.SetTotalColons(newValue)
      },
      stopDrag() {
          this.isDragging = false;
          document.removeEventListener('mousemove', this.onDrag);
          document.removeEventListener('mouseup', this.stopDrag);
          document.removeEventListener('touchmove', this.onDrag);
          document.removeEventListener('touchend', this.stopDrag);
      },
      showValue() {
          this.valueVisible = true;
      },
      hideValue() {
          this.valueVisible = false;
      },
      setValue(event) {
          const sliderRect = this.$el.querySelector('.slider').getBoundingClientRect();
          const offsetX = event.clientX - sliderRect.left; // Получаем x-координату относительно ползунка
          let newValue = Math.round((offsetX / this.sliderWidth) * this.maxValue);
          // Ограничиваем значение между 0 и maxValue
          newValue = Math.max(0, Math.min(newValue, this.maxValue));
          this.SetTotalColons(newValue)
      },
  },
  name: 'my-slider'
};
</script>

<style lang="scss" scoped>
.slider-container {
  display: flex;
  align-items: center;
}

.slider {
  position: relative;
  width: 220px; /* Установите ширину ползунка */
  height: 4px;
  background-color: #414141; /* Серый фоновый цвет */
  margin: 0 10px;
  border-radius: 2px;
}

.slider-thumb {
  position: absolute;
  width: 14px;
  height: 14px;
  background-color: #414141;/* Серый цвет кружка */
  border: 2px solid #6d68e4; /* Фиолетовая рамка */
  border-radius: 50%;
  cursor: pointer;
  transition: background-color 0.2s;
  z-index: 3;
  top: -5px;
}

.slider-fill {
  position: absolute;
  height: 100%;
  background-color: #6d68e4; /* Фиолетовый цвет */
  left: 0;
  top: 0;
}
.value-display {
  position: absolute;
  top: -70px;
  padding: 7px 5px;
  background-color: black;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  &::after{
    content: ''; 
    position: absolute; /* Абсолютное позиционирование */
    top: 100%; /* Положение треугольника */
    border: 5px solid transparent; /* Прозрачные границы */
    border-top: 5px solid black; /* Добавляем треугольник */
  }
}
button {
  margin: -5px 5px 0;
  cursor: pointer;
  background: transparent;
  color: white;
  font-family: Mulish;
  font-size: 16px;
  font-weight: 400;
}
</style>