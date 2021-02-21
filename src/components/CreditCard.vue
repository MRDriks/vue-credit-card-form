<template>
  <div class="credit-card">
    <div class="card-face credit-card-front">
      <img src="@/assets/img/chip.png" class="img-chip" alt="Credit card chip">
      <img src="@/assets/img/visa.png" class="img-visa img-visa-front" alt="Credit card visa">
      <div class="card-number">
        <span v-for="(num, index) in cardNumber" v-bind:key="index">{{ num }}</span>
      </div>
      <div class="card-holder">
        <span class="title">Card Holder</span>
        <p class="full-name text">{{ fullName }}</p>
      </div>
      <div class="card-expires">
        <span class="title">Expires</span>
        <p class="date text">{{ cardExpiry.month }}/{{ cardExpiry.year }}</p>
      </div>
    </div>
    <div class="card-face credit-card-back">
      <div class="card-cvv">
        <span class="title-cvv">Cvv</span>
        <div class="cvv-strip">
          <span class="cvv-number">{{ cvvCode }}</span>
        </div>
      </div>
      <img src="@/assets/img/visa.png" class="img-visa img-visa-back" alt="Credit card visa">
    </div>
  </div>
</template>

<script>
export default {
  name: 'CreditCard',

  props: {
    cardExpiry: {
      type: Object,
      default() {
        return {
          month: 'MM',
          year: 'YY',
        };
      },
    },

    fullName: {
      type: String,
      default: 'Full Name',
    },

    cardNumber: {
      type: Array,
    },

    cvvCode: {
      type: String,
      default: '',
    },
  },
};
</script>

<style scoped>
.credit-card {
  position: absolute;
  top: 50px;
  width: 430px;
  height: 270px;
  border-radius: 15px;
  color: #fff;
  font-family: "Source Code Pro", monospace;
  font-weight: 500;
  text-shadow: 7px 6px 10px rgb(14 42 90 / 80%);
  transition: transform 1s;
  perspective: 1000px;
}

.flip.credit-card-front {
  transform: rotateY(180deg);
}

.flip.credit-card-back {
  transform: rotateY(360deg);
}

.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  border-radius: 15px;
  backface-visibility: hidden;
  transition: transform 1s ease-in-out;
  background-image: url(../assets/img/1.jpeg);
  background-position: center center;
  box-shadow: 0 20px 60px 0 rgb(14 42 90 / 55%);
}

.credit-card-back {
  transform: rotateY(180deg);
}

.credit-card-front::before,
.credit-card-back::before  {
  content: '';
  display: block;
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 15px;
  z-index: 1;
}

.credit-card-back::after {
  content: '';
  display: block;
  width: 100%;
  position: absolute;
  top: 30px;
  left: 0;
  height: 50px;
  background-color: rgba(0, 0, 0, 0.9)
}

.card-cvv {
  width: 92%;
  position: absolute;
  z-index: 2;
  top: 100px;
  left: 15px;
}

.title-cvv {
  text-transform: uppercase;
  color: #fff;
  display: block;
  text-align: right;
  margin-bottom: 5px;
  padding-right: 10px;
  font-weight: 400;
}

.cvv-strip {
  width: 100%;
  height: 50px;
  background-color: #fff;
  border-radius: 5px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.cvv-number {
  margin-right: 10px;
  text-shadow: none;
  color: #000;
}

.credit-card::after {
  content: '';
  display: block;
  position: absolute;
  border: 2px solid #fff;
  border-radius: 15px;
  width: 100%;
  height: 100%;
  z-index: 1;
  opacity: 0;
  transition: all 1s ease;
}

.card-number-focus.credit-card::after {
  width: 90%;
  height: 15%;
  transform: translate(22px, 113px);
  opacity: 1;
}

.date-focus.credit-card::after {
  transform: translate(320px, 200px);
  width: 22%;
  height: 20%;
  opacity: 1;
}

.full-name-focus.credit-card::after {
  transform: translate(10px, 200px);
  width: 69%;
  height: 18%;
  opacity: 1;
}

.img-chip {
  top: 25px;
  position: absolute;
  z-index: 2;
}

.img-visa {
  width: 85px;
  height: 45px;
  right: 25px;
  position: absolute;
  z-index: 2;
}

.img-visa-front {
  top: 25px;
}

.img-visa-back {
  bottom: 25px;
}

.img-chip {
  width: 60px;
  height: 48px;
  left: 25px;
}

.card-number {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  font-size: 27px;
  z-index: 2;
  display: flex;
}

.card-number span:nth-child(4),
.card-number span:nth-child(8),
.card-number span:nth-child(12) {
  margin-right: 30px;
}

.card-holder,
.card-expires {
  position: absolute;
  z-index: 2;
  bottom: 25px;
}

.card-holder {
  left: 25px;
}

.card-expires {
  right: 25px;
}

.title {
  opacity: 0.7;
  font-size: 13px;
  margin-bottom: 6px;
}

.text {
  font-size: 18px;
  text-transform: uppercase;
}
</style>
