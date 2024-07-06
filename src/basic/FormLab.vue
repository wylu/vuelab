<template>
  <!-- 文本 -->
  <p>Message is: {{ message }}</p>
  <input v-model="message" placeholder="edit me" />

  <!-- 多行文本 -->
  <p>Multiline message is:</p>
  <p style="white-space: pre-line">{{ multilineMessage }}</p>
  <textarea v-model="multilineMessage" placeholder="add multiple lines"></textarea>

  <!-- 复选框 -->
  <p></p>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">{{ checked }}</label>

  <p></p>
  <div>Checked names: {{ checkedNames }}</div>

  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>

  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>

  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>

  <!-- 单选按钮 -->
  <p></p>
  <div>Picked: {{ picked }}</div>

  <input type="radio" id="one" value="One" v-model="picked" />
  <label for="one">One</label>

  <input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>

  <!-- 选择器 -->
  <p></p>
  <div>Selected: {{ selected }}</div>

  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>

  <p></p>
  <div>Multiple selected: {{ multipleSelected }}</div>

  <select v-model="multipleSelected" multiple>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>

  <p></p>
  <div>Dynamic selected: {{ dynamicSelected }}</div>

  <select v-model="dynamicSelected">
    <option v-for="option in dynamicOptions" :key="option.text" :value="option.value">
      {{ option.text }}
    </option>
  </select>

  <!-- 值绑定 -->
  <p></p>
  <div>Checked value: {{ toggleCheckbox1 }}</div>
  <input
    type="checkbox"
    id="toggle-checkbox1"
    v-model="toggleCheckbox1"
    true-value="yes"
    false-value="no"
  />
  <label for="toggle-checkbox1">{{ toggleCheckbox1 }}</label>

  <p></p>
  <div>Checked value: {{ toggleCheckbox2 }}</div>
  <input
    type="checkbox"
    id="toggle-checkbox2"
    v-model="toggleCheckbox2"
    :true-value="toggleCheckbox2Yes"
    :false-value="toggleCheckbox2No"
  />
  <label for="toggle-checkbox2">{{ toggleCheckbox2 }}</label>

  <p></p>
  <div>Picked value: {{ pickRadio }}</div>
  <input type="radio" id="pick-first" v-model="pickRadio" :value="first" />
  <label for="pick-first">{{ first }}</label>
  <input type="radio" id="pick-second" v-model="pickRadio" :value="second" />
  <label for="pick-second">{{ second }}</label>

  <p></p>
  <div>Selected value: {{ pickSelect }}</div>
  <select v-model="pickSelect">
    <!-- 内联对象字面量 -->
    <option :value="{ number: 123 }">123</option>
  </select>

  <!-- 修饰符 -->
  <p></p>
  <div>msg: {{ msg }}</div>
  <input v-model.lazy="msg" />

  <p></p>
  <div>age type: {{ typeof age }}</div>
  <div>age value: {{ age }}</div>
  <input v-model.number="age" />

  <p></p>
  <div>content: "{{ content }}"</div>
  <input v-model.trim="content" />
</template>

<script setup lang="ts">
import { ref } from 'vue'

const message = ref('')

const multilineMessage = ref('')

const checked = ref(false)

const checkedNames = ref([])

const picked = ref('')

const selected = ref('')

const multipleSelected = ref('')

const dynamicSelected = ref('A')
const dynamicOptions = ref([
  { text: 'One', value: 'A' },
  { text: 'Two', value: 'B' },
  { text: 'Three', value: 'C' }
])

const toggleCheckbox1 = ref('')

const toggleCheckbox2 = ref('')
const toggleCheckbox2Yes = ref('yes')
const toggleCheckbox2No = ref('no')

const pickRadio = ref('')
const first = ref('first')
const second = ref('second')

const pickSelect = ref('')

const msg = ref('')
const age = ref('')
const content = ref('')
</script>
