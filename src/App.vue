<template>
  <div id="app">
    <div class="container">
      <div class="section">
        {{ message }}
        <h3>Input Field</h3>
        <input v-model="message" placeholder="Input Placeholder" />

        <h3>Input Field Focus</h3>
        <input ref="name" />

        <h3>Input Error</h3>
        <input type="text" v-model="input" class="p-invalid">

        <h3>Input Disabled Field</h3>
        <input type="text" v-model="inputValue" :disabled="isDisabled">
        <button @click="toggleDisabled">Disabled</button>

        <h3>Number Input Field</h3>
        <input type="number" v-model.number="numberValue">

        <h3>TextArea</h3>
        <textarea v-model="textAreaValue" rows="4" cols="50"></textarea>
      </div>
      <div class="section">

        <h3>DropdownwithSearch</h3>
        <v-select v-model="selectedOption" :options="options" :searchable="true" aria-placeholder="Dropdown Select" />

        <h3>Calender</h3>
        <input type="date" v-model="mydate" dateFormat="dd/mm/yy" />
        {{ mydate }}

        <h3>Toast</h3>


      </div>
      <div class="section">
        <h3>Toast</h3>
        <input type="file" multiple @change="handleFileChange" />
        <div v-for="(file, index) in files" :key="index">
          <div>{{ file.name }}</div>
          <div>{{ file.time }}</div>
          <button @click="removeFile(index)">❌</button>
        </div>

        <h3>Chips</h3>
        <Chips v-model="value" />
        <div>

          <h3>Toggle</h3>
          <button @click="toggle">Toggle</button>

          <h3>CheckBox</h3>
          <input type="checkbox" v-model="isChecked" @change="handleChange">
          <input type="checkbox" v-model="isChecked" @change="handleChange">

          <h3>RadioButton</h3>
          <input type="radio" id="option1" value="option1" v-model="selectedOption" @change="handleChange">
          <input type="radio" id="option2" value="option2" v-model="selectedOption" @change="handleChange">
          <input type="radio" id="option3" value="option3" v-model="selectedOption" @change="handleChange">

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import vSelect from 'vue-select';
import 'vue-select/dist/vue-select.css';



export default {
  name: 'App',
  components: {
    'v-select': vSelect,
  },
  mounted() {
    this.focusInput();
  },
  methods: {
    focusInput() {
      this.$refs.name.focus();
    },
    toggleDisabled() {
      this.isDisabled = !this.isDisabled;
    },

    handleFileChange(event) {
      const fileList = event.target.files;
      for (let i = 0; i < fileList.length; i++) {
        const file = fileList[i];
        this.files.push({ name: file.name, time: new Date().toLocaleString() });
      }
    },
    removeFile(index) {
      this.files.splice(index, 1);
    },

  },
  data() {
    return {
      inputValue: '',
      isDisabled: false,
      numberValue: 0,
      files: [],

      selectedOption: null,
      options: [
        { label: 'item1', value: 'option1' },
        { label: 'item2', value: 'option2' },
        { label: 'item3', value: 'option3' },
        // Add more options as needed
      ]
    };
  },

}
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  display: flex;
  height: 100%;
  /* Adjust as needed */
}

.section {
  flex: 1;
  border: 1px solid #ccc;
  padding: 120px;

}
</style>
