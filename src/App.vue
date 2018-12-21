<template>
  <div id="app" class="app">
    <div class="container">
      <img alt="Odyzeo logo" src="./assets/logo.png">

      <h2>
        odyzeo/form-item
        <br>
        <a href="https://www.npmjs.com/package/@odyzeo/form-item" target="_blank" class="link-icon">
          <img alt="NPM logo" src="./assets/npm.svg" class="icon icon-npm">
        </a>
        <a href="https://github.com/odyzeo/form-item" target="_blank" class="link-icon">
          <img alt="Github logo" src="./assets/github.svg" class="icon icon-github">
        </a>
      </h2>
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

      <h2>
        odyzeo/form-radio
        <br>
        <a href="https://www.npmjs.com/package/@odyzeo/form-radio" target="_blank" class="link-icon">
          <img alt="NPM logo" src="./assets/npm.svg" class="icon icon-npm">
        </a>
        <a href="https://github.com/odyzeo/form-radio" target="_blank" class="link-icon">
          <img alt="Github logo" src="./assets/github.svg" class="icon icon-github">
        </a>
      </h2>
      <form-radio
        :input="radio"
        v-model="radio.value"
        :form-errors="formErrors[radio.name]"
      ></form-radio>

      <p>
        Model: {{radio.value}}
      </p>

      <h2>
        odyzeo/form-checkbox
        <br>
        <a href="https://www.npmjs.com/package/@odyzeo/form-checkbox" target="_blank" class="link-icon">
          <img alt="NPM logo" src="./assets/npm.svg" class="icon icon-npm">
        </a>
        <a href="https://github.com/odyzeo/form-checkbox" target="_blank" class="link-icon">
          <img alt="Github logo" src="./assets/github.svg" class="icon icon-github">
        </a>
      </h2>
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

      <h2>
        odyzeo/form-autocomplete - single
        <br>
        <a href="https://www.npmjs.com/package/@odyzeo/form-autocomplete" target="_blank" class="link-icon">
          <img alt="NPM logo" src="./assets/npm.svg" class="icon icon-npm">
        </a>
        <a href="https://github.com/odyzeo/form-autocomplete" target="_blank" class="link-icon">
          <img alt="Github logo" src="./assets/github.svg" class="icon icon-github">
        </a>
      </h2>
      <form-autocomplete
        v-model="selectedItems"
        :label="'Participants'"
        :placeholder="'Type to search'"
        :options="filteredItems"
        :option-id="'name'"
        :loading="isSearchLoading"
        :hide-selected="true"
        :select-first="true"
        @search-change="search"
      >
        <template
          slot="tag"
          slot-scope="props"
        >
          {{ props.item.name }}
        </template>
        <template
          slot="item"
          slot-scope="props"
        >
          {{ props.item.name }}
        </template>
        <template slot="no-results">
          Participants not found
        </template>
        <template slot="loading">
          ...loading...
        </template>
      </form-autocomplete>

      <p>Model:</p>
      <p>
        {{selectedItems}}
      </p>

      <h2>odyzeo/form-autocomplete - tags</h2>
      <form-autocomplete
        v-model="selectedTagItems"
        :label="'Participants'"
        :placeholder="'Type to search'"
        :options="filteredItems"
        :option-id="'name'"
        :loading="isSearchLoading"
        :hide-selected="true"
        :tags="true"
        :select-first="true"
        @search-change="search"
      >
        <template
          slot="tag"
          slot-scope="props">
          {{ props.item.name }}
        </template>
        <template
          slot="item"
          slot-scope="props">
          {{ props.item.name }}
        </template>
        <template slot="no-results">
          Participants not found
        </template>
        <template slot="loading">
          ...loading...
        </template>
      </form-autocomplete>

      <p>Model:</p>
      <p>
        {{selectedTagItems}}
      </p>

    </div>
  </div>
</template>

<script>
import FormAutocomplete from '@odyzeo/form-autocomplete'
import FormCheckbox from '@odyzeo/form-checkbox'
import FormItem from '@odyzeo/form-item'
import FormRadio from '@odyzeo/form-radio'

export default {
  name: 'app',
  components: {
    FormAutocomplete,
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
      selectedItems: [],
      selectedTagItems: [
        { name: 'Zombi' },
      ],
      items: [
        { name: 'Denton' },
        { name: 'Pe4k' },
        { name: 'PaDi' },
        { name: 'Zoli' },
        { name: 'Zombi' },
      ],
      filteredItems: [],
      isSearchLoading: false,
    }
  },
  methods: {
    search (query) {
      this.filteredItems = []
      this.isSearchLoading = true

      if (query.length < this.minSearchLength) {
        return
      }

      this.startSearching(query)
    },
    startSearching (query) {
      this.filteredItems = this.items.filter(item =>
        item.name.toLowerCase()
          .includes(query.toLowerCase()))
      this.isSearchLoading = false
    },
  },
}
</script>

<style lang="less">
@import "~normalize.css";
@import '~@odyzeo/form-item/dist/form-item.css';
@import '~@odyzeo/form-autocomplete/dist/form-autocomplete.css';
@import '~@odyzeo/form-checkbox/dist/form-checkbox.css';
@import '~@odyzeo/form-radio/dist/form-radio.css';
@import './less/app.less';

h2 {
  margin-top: 2em;
}

.form-radio,
.form-checkbox {
  margin: 5px 0;
}

.link-icon {
  display: inline-block;
  padding: 5px;
}

.icon {
  vertical-align: middle;
}

.icon-github {
  width: 20px;
}

.icon-npm {
  width: 30px;
}
</style>
