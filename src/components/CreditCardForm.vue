<template>
  <form class="credit-card-form">
    <div class="input-group">
      <label class="label" for="input_card_number">Card Number</label>
      <input
        type="text"
        id="input_card_number"
        maxlength="16"
        v-on:keypress="validateNumbersInput"
        v-on:input="$emit('changeCardNumber', $event.target.value)"
        v-on:focus="handleCardNumberFocus"
        v-on:blur="handleCardNumberBlur">
    </div>
    <div class="input-group">
      <label class="label" for="input_card_holder">Card Holder</label>
      <input
        type="text"
        id="input_card_holder"
        maxlength="26"
        v-on:input="$emit('changeFullName', $event.target.value)"
        v-on:focus="handleFullNameFocus"
        v-on:blur="handleFullNameBlur">
    </div>
    <div class="row">
      <div class="input-group">
        <label class="label" for="select_month">Expiration Date</label>
        <div class="row">
          <select
            class="select-month"
            id="select_month"
            v-on:change="$emit('changeMonth', $event.target.value)"
            v-on:focus="handleExpirationDateFocus"
            v-on:blur="handleExpirationDateBlur">
              <option selected disabled>Month</option>
              <option
                v-for="item in months"
                v-bind:key="item"
                v-bind:value="item">
                  {{ item }}
              </option>
          </select>
          <select
            class="select-year"
            v-on:change="$emit('changeYear', $event.target.value)"
            v-on:focus="handleExpirationDateFocus"
            v-on:blur="handleExpirationDateBlur">
              <option selected disabled>Year</option>
              <option
                v-for="item in years"
                v-bind:key="item"
                v-bind:value="item">
                  {{ item }}
              </option>
          </select>
        </div>
      </div>
      <div class="input-group">
        <label class="label" for="input_cvv">CVV</label>
        <input
          type="password"
          id="input_cvv"
          maxlength="3"
          v-on:keypress="validateNumbersInput"
          v-on:input="$emit('changeCvv', $event.target.value)"
          v-on:focus="handleCvvFocus"
          v-on:blur="handleCvvBlur">
      </div>
    </div>
    <button class="btn-submit" type="button">Submit</button>
  </form>
</template>

<script>
export default {
  name: 'CreditCardForm',

  data() {
    return {
      months: ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'],
      years: [2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030, 2031, 2032],
    };
  },

  methods: {
    validateNumbersInput(event) {
      const code = event.keyCode;
      if (code < 48 || code > 57) {
        event.preventDefault();
      }
    },

    addStyleClass(element, className) {
      const el = document.querySelector(`.${element}`);
      el.classList.add(`${className}`);
    },

    removeStyleClass(element, className) {
      const el = document.querySelector(`.${element}`);
      el.classList.remove(`${className}`);
    },

    handleFullNameFocus() {
      this.addStyleClass('credit-card', 'full-name-focus');
    },

    handleFullNameBlur() {
      this.removeStyleClass('credit-card', 'full-name-focus');
    },

    handleCardNumberFocus() {
      this.addStyleClass('credit-card', 'card-number-focus');
    },

    handleCardNumberBlur() {
      this.removeStyleClass('credit-card', 'card-number-focus');
    },

    handleExpirationDateFocus() {
      this.addStyleClass('credit-card', 'date-focus');
    },

    handleExpirationDateBlur() {
      this.removeStyleClass('credit-card', 'date-focus');
    },

    handleCvvFocus() {
      this.addStyleClass('credit-card-front', 'flip');
      this.addStyleClass('credit-card-back', 'flip');
    },

    handleCvvBlur() {
      this.removeStyleClass('credit-card-front', 'flip');
      this.removeStyleClass('credit-card-back', 'flip');
    },
  },
};
</script>

<style scoped>
.credit-card-form {
  width: 570px;
  background-color: #fff;
  padding: 180px 35px 35px 35px;
  box-shadow: 0 30px 60px 0 rgb(90 116 148 / 40%);
  border-radius: 10px;
  margin-top: 135px;
}

.credit-card-form > .input-group:nth-child(2) {
  margin: 20px 0;
}

.row {
  display: flex;
  justify-content: space-between;
}

.label {
  font-size: 14px;
  margin-bottom: 5px;
  font-weight: 500;
  color: #1a3b5d;
}

.input-group {
  display: flex;
  flex-direction: column;
}

input,
select {
  height: 50px;
  border: 1px solid #ced6e0;
  border-radius: 5px;
  transition: border 0.3s linear;
}

input:hover,
select:hover,
input:focus,
select:focus {
  border: 1px solid #2364d2;
}

input,
select,
option {
  font-size: 18px;
  padding: 5px 15px;
  color: #1a3b5d;
  font-family: "Source Sans Pro", sans-serif;
}

#input_cvv,
.select-month,
.select-year {
  width: 150px;
}

.select-month {
  margin-right: 15px;
}

.btn-submit {
  width: 100%;
  height: 55px;
  border: none;
  background-color: #2364d2;
  color: #fff;
  font-size: 22px;
  border-radius: 5px;
  box-shadow: 3px 10px 20px 0px rgb(35 100 210 / 30%);
  font-weight: 500;
  font-family: "Source Sans Pro", sans-serif;
  margin-top: 35px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-submit:hover {
  background-color: #144eb3;
}
</style>
