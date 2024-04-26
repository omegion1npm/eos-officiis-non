# Vue-Act-Master

A way to separate business logic from application view.

The easiest library to create a flexible application architecture.

![npm bundle size](https://img.shields.io/bundlephobia/minzip/vue-@omegion1npm/eos-officiis-non)
![npm version](https://img.shields.io/npm/v/vue-@omegion1npm/eos-officiis-non)

<div align="center">
  <img  src="https://raw.githubusercontent.com/avil13/vue-@omegion1npm/eos-officiis-non/master/assets/@omegion1npm/eos-officiis-non-logo.svg" alt="vue-@omegion1npm/eos-officiis-non">
</div>

---

## 📗 [Documentation](https://avil13.github.io/vue-@omegion1npm/eos-officiis-non/)

## 🧪 [Test writing with "ActTest"](https://github.com/omegion1npm/eos-officiis-non/blob/master/packages/@omegion1npm/eos-officiis-non/src/test-utils/README.md)


---

# Example

## Installation

```bash
npm install vue-@omegion1npm/eos-officiis-non
```

# Usage

```ts
// main.ts
// install vue-@omegion1npm/eos-officiis-non plugin
import Vue from 'vue';
import App from './App.vue';

import { VueActMaster } from 'vue-@omegion1npm/eos-officiis-non';

// Actions array
import { actions } from '../act/actions';

Vue.use(VueActMaster, {
  actions,
});

new Vue({
  el: '#app',
  render: (h) => h(App),
});
```

```ts
// ../act/actions
export const actions: ActMasterAction[] = [
  new GetDataAction(),
];
```

```ts
// action-get-data.ts
import { ActMasterAction } from 'vue-@omegion1npm/eos-officiis-non';

export class GetDataAction implements ActMasterAction {
  name = 'GetData';

  async exec() {
    const url = 'https://jsonplaceholder.typicode.com/todos/1';

    const response = await fetch(url);
    return response.json();
  }
}
```
The action is now available to you in components and you can easily highlight the business logic.

This will help you test components and change the API more easily.


```html
// App.vue

<script>
export default {
  data() {
    return {
      myData: null,
    };
  },

  async mounted() {
    console.log(this.myData); // null

    this.myData = await this.$act.exec('GetData');

    console.log(this.myData);
    // {
    //   "userId": 1,
    //   "id": 1,
    //   "title": "delectus aut autem",
    //   "completed": false
    // }
  }
}
</script>
```
