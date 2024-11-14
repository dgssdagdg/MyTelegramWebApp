<template>
  <Navbar/>
  <div class="home">
    <div class="container">
      <div class="home-row">
        <div class="home-content">
          <div class="home-sub-title">Текст в изображение</div>
          <h1 class="home-title">Insomnia AI Генератор изображений</h1>
          <p class="home-text">Интеграция различных моделей искусственного интеллекта позволяет реализовать ваши творческие идеи в одном месте, экономя ваше время и усилия.</p>
          <a href="#" class="home-btn">Творить самостоятельно еееее 👉</a>
        </div>
        <my-slider/>
        <div ref="observedBlock" class="image-grid">
          <img
            :key="item.url"
            v-for="(item, index) in images"
            :src="item.url"
            :height="item.heigth"
            :width="blockWidth / totalColons"
            alt="Image 1"
            :style="getTransformStyle(index)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from './views/Navbar';
import { mapState } from 'vuex';
export default {
  data() {
    return {
      images: [
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/ca88756c-cebb-49fa-83f8-8eb183204e33.jpeg', heigth: 250},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/12abcef5-2c24-450f-9f0b-b815fa25788d_0.jpeg', heigth: 350},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/2b7ea5de-6f81-4ebe-b598-f3c12fbc7ac7_0.jpeg', heigth: 250},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/ef0015c7-3465-4b11-8ae7-2df3909ff911_0.jpeg', heigth: 250},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/312fa878-47a8-427f-b1df-b789faa20f17_0.jpeg', heigth: 350},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/29b7c447-2260-4c21-852d-eb129429d420_2.jpeg', heigth: 350},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/176400fb-ba36-4440-912f-098118d1aff9_0.jpeg', heigth: 250},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/76cd4f06-abb9-4120-b96f-0a895d6e4f19.jpeg', heigth: 250},
        {url:'https://d3h9mjt2kldmtl.cloudfront.net/12abcef5-2c24-450f-9f0b-b815fa25788d_0.jpeg', heigth: 350},
      ],
      startWidth: 0,
      blockWidth: 0, // Начальная ширина блока
    }
  },
  components: {
    Navbar
  },
  computed: {
    ...mapState({
      totalColons: state => state.home.totalColons,
    }),
  },
  mounted() {
    // Убедитесь, что Telegram Web App загружен
    if (window.Telegram && window.Telegram.WebApp) {
      this.initTelegram();
    } else {
      console.error('Telegram Web App не доступен');
    }

    // Создаем экземпляр ResizeObserver
    this.resizeObserver = new ResizeObserver((entries) => {
      for (let entry of entries) {
        // Обновляем ширину блока при изменении
        this.blockWidth = entry.contentRect.width;
      }
    });

    // Начинаем наблюдение за элементом
    this.resizeObserver.observe(this.$refs.observedBlock);
  },
  beforeDestroy() {
    // Отключаем наблюдатель, когда компонент уничтожается
    if (this.resizeObserver) {
      this.resizeObserver.unobserve(this.$refs.observedBlock);
    }
  },
  methods: {
    initTelegram() {
      // Инициализация процесса работающего с Telegram Web App
      window.Telegram.WebApp.ready();
    },
    getTransformStyle(index) {
      console.log(this.totalColons);
      
      const rowIndex = Math.floor(index / this.totalColons); // Находим текущий ряд
      const colIndex = index % this.totalColons; // Находим индекс в ряду
      let translateX = (this.blockWidth / this.totalColons * colIndex) + colIndex * 6; // Вычисляем значение трансформации
      let topHeigth = 0;
      for(let i = rowIndex; i > 0; i--) {
        topHeigth += this.images[index - (this.totalColons * i)].heigth;
      }
      if(topHeigth != 0){topHeigth += 6 * rowIndex}
      return {
        transform: `translate3d(${translateX}px, ${topHeigth}px, 0px)`,
      };
    },
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Mulish:ital,wght@0,200..1000;1,200..1000&display=swap');
*{
    padding: 0;
    margin: 0;
    border: 0;
}
*,*:before,*:after{
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
:focus,:active{outline: none;}
a:focus,a:active{outline: none;}
nav,footer,header,aside{display:block;}
html,body{height: 100%;width: 100%;font-size: 100%;line-height: 1;font-size: 14px;-ms-text-size-adjust: 100%;-moz-text-size-adjust: 100%;-webkit-text-size-adjust: 100%;}
input,button,textarea{font-family: inherit;}
input::-ms-clear{display: none;}
button{cursor: pointer;}
button::-moz-focus-inner{padding: 0;border: 0;}
a,a:visited{text-decoration: none;}
a:hover{text-decoration: none;}
ul li{list-style: none;}
img{vertical-align: top;}
h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight: inherit;}
body {
  font-family: Mulish;
  color: #fff;
  & a {
    color: #fff;
  }
}
.container {
    padding: 0 21px;
}
.home {
  padding: 42px 0 0;
}
.home-row {
}
.home-content {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 30px;
}
.home-sub-title {
  font-weight: 700;
  font-size: 20px;
  line-height: calc(28 / 22 * 100%);
  color: rgb(98, 101, 238);
}
.home-title {
  margin: 6px 0px 0px;
  font-weight: 700;
  line-height: 140%;
  font-size: 26px;
}
.home-text {
  font-weight: 400;
  font-size: 16px;
  line-height: 170%;
  margin: 10px 0px 0px;
  max-width: 350px;
}
.home-btn {
  padding: 14px 25px;
  border: none;
  background-color: rgb(98, 101, 238);
  border-radius: 30px;
  cursor: pointer;
  color: rgb(255, 255, 255);
  font-weight: 600;
  font-size: 18px;
  line-height: 23px;
  margin-top: 21px;
}
.image-grid {
  position: relative;
  width: 100%;
  height: 100%;
  margin-top: 30px;
}

.image-grid img {
  position: absolute;
  object-fit: cover;
  will-change: transform, width, height, opacity;
  border-radius: 10px;
}
</style>