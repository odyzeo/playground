<template>
  <div id="app">
    <div class="container">
      <img alt="Odyzeo logo" src="./assets/logo.png">

      <h2>odyzeo/form-item</h2>
      <form-item
        :input="simple"
        v-model="simple.value"
      ></form-item>
      <p>
        Model: {{simple.value}}
      </p>

      <form-item
        :input="full"
        v-model="full.value"
        :msg-required="requiredMessage"
        :form-errors="formErrors.full"
        class="form-item--group"
      >
        <template slot="prepend">
          <div class="form-item__readonly">Your</div>
        </template>
        <template slot="append">
          <div class="form-item__readonly">Please</div>
        </template>
      </form-item>
      <p>
        Model: {{full.value}}
      </p>

      <h2>odyzeo/form-radio</h2>
      <form-radio
        :input="radio"
        v-model="radio.value"
        :form-errors="formErrors[radio.name]"
      ></form-radio>

      <p>
        Model: {{radio.value}}
      </p>

      <h2>odyzeo/form-checkbox</h2>
      <form-checkbox
        v-for="(checkbox, key) in checkboxes"
        :input="checkbox"
        :key="`${checkbox.name}-${checkbox.value}-${key}`"
        v-model="checkbox.value"
        :form-errors="formErrors[checkbox.name]"
      ></form-checkbox>

      <p>Model:</p>
      <div
        v-for="(checkbox, key) in checkboxes"
        :key="`${checkbox.name}-${checkbox.value}-${key}`"
      >
        {{checkbox.label}}: {{checkbox.value}}
      </div>
    </div>
  </div>
</template>

<script>
import FormCheckbox from '@odyzeo/form-checkbox'
import FormItem from '@odyzeo/form-item'
import FormRadio from '@odyzeo/form-radio'

export default {
  name: 'app',
  components: {
    FormCheckbox,
    FormItem,
    FormRadio,
  },
  data () {
    return {
      checkboxes: [
        {
          name: 'checkbox_ios',
          label: 'iOS',
          value: true,
        },
        {
          name: 'checkbox_android',
          label: 'Android',
        },
        {
          name: 'checkbox_windows',
          label: 'Windows',
          value: false,
        },
      ],
      simple: {
        label: 'Simple',
        value: '',
      },
      full: {
        type: 'email',
        name: 'email',
        required: true,
        readonly: false,
        placeholder: 'example@odyzeo.com',
        accept: '', // Just for input type 'file'
        validators: ['email'],
        rows: 0, // Just for input type 'textarea'
        autocomplete: 'username email',
        label: 'E-mail',
        value: '',
      },
      requiredMessage: 'Povinné',
      formErrors: {},
      radio: {
        name: 'platform',
        value: 'android',
        options: [
          {
            value: 'ios',
            name: 'iOS',
          },
          {
            value: 'android',
            name: 'Android',
          },
          {
            value: 'windows',
            name: 'Windows Phone',
          },
        ],
      },
    }
  },
}
</script>

<style lang="less">
@import "~normalize.css";
@import '~@odyzeo/form-item/dist/form-item.css';
@import '~@odyzeo/form-checkbox/dist/form-checkbox.css';
@import '~@odyzeo/form-radio/dist/form-radio.css';
@import './less/app.less';

.form-radio,
.form-checkbox {
  margin: 5px 0;
}

;
</style>
