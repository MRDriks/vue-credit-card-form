<template>
  <div id="app">
    <div class="container">
      <CreditCard
        v-bind:card-expiry="cardExpiry"
        v-bind:full-name="fullName"
        v-bind:card-number="cardNumber"
        v-bind:cvv-code="cvv" />
      <CreditCardForm
        v-on:changeMonth="handleMonthChange($event)"
        v-on:changeYear="handleYearChange($event)"
        v-on:changeFullName="handleFullNameChange($event)"
        v-on:changeCardNumber="handleCardNumberChange($event)"
        v-on:changeCvv="handleCvvChange($event)" />
    </div>
  </div>
</template>

<script>
import CreditCard from '@/components/CreditCard.vue';
import CreditCardForm from '@/components/CreditCardForm.vue';

export default {
  name: 'App',

  components: {
    CreditCard,
    CreditCardForm,
  },

  data() {
    return {
      cardExpiry: {
        month: 'MM',
        year: 'YY',
      },
      fullName: 'Full Name',
      cardNumber: [],
      cvv: '',
    };
  },

  created() {
    const defaultCardNumber = '#'.repeat(16);
    const defaultCardNumberArr = defaultCardNumber.split('');
    this.cardNumber = defaultCardNumberArr;
  },

  methods: {
    handleMonthChange(month) {
      this.cardExpiry.month = month;
    },

    handleYearChange(year) {
      this.cardExpiry.year = year;
    },

    handleFullNameChange(fullName) {
      this.fullName = fullName;
    },

    handleCardNumberChange(number) {
      const numsArray = number.padEnd(16, '#').split('');
      this.cardNumber = numsArray;
    },

    handleCvvChange(cvv) {
      const hiddenNum = '*'.repeat(cvv.length);
      this.cvv = hiddenNum;
    },
  },
};
</script>

<style scoped>
#app {
  background: #ddeefc;
  font-family: "Source Sans Pro", sans-serif;
  font-size: 16px;
  padding: 50px 15px;
}

.container {
  display: flex;
  justify-content: center;
}
</style>
