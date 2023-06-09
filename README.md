## vue-pithy-pagination 重构

### vue-pithy-pagination@0.1.2 发现在vue3中使用不了，因为是2年前编写的组件库，使用webpack进行打包构建，可能一些构建上的语法不兼容vue3，这次重构就用了rollup进行打包构建，进测试，兼容vue2和vue3，且包体积减少了。

### vue-pithy-pagination@0.1.2

**下载**

```bash
npm i vue-pithy-pagination@0.1.2 -D
```


**使用**
```js
<template>
   <div id="app">
    <vue-pithy-pagination
      :allCount="allCount"
      :pageCount="pageCount"
      @getCurrentPage="getCurrentPage"
      @choosePage="choosePage"
    />
  </div>
</template>
<script>
import VuePithyPagination from 'vue-pithy-pagination'

import 'vue-pithy-pagination/dist/vue-pithy-pagination.css'
export default {
  name: "App",
  data() {
    return {
      allCount: 101,
      pageCount: 10,
    };
  },
    components:{VuePithyPagination},

  methods: {
    getCurrentPage(currentPage) {
      console.log(currentPage);
    },
    choosePage(pageCount) {
      this.pageCount = pageCount;
    },
  },
}
</script>
```


## 重构版本

### vue-pithy-pagination@latest

**下载**

```bash
npm i vue-pithy-pagination@latest -D
```

**使用**
```js
//vue2
<template>
    <div id="app">
    <vue-pithy-pagination
      :allCount="allCount"
      :pageCount="pageCount"
      @getCurrentPage="getCurrentPage"
      @choosePage="choosePage"
    />
  </div>
</template>
<script>
import VuePithyCalendar from 'vue-pithy-calendar/dist/vue2/esm'

export default {
  name: "App",
  data() {
    return {
      allCount: 101,
      pageCount: 10,
    };
  },
components:{VuePithyPagination},
 
  methods: {
    getCurrentPage(currentPage) {
      console.log(currentPage);
    },
    choosePage(pageCount) {
      this.pageCount = pageCount;
    },
  },
}
</script>

```

```js
//vue3
<template>
    <div>
        <vue-pithy-pagination
      :allCount="allCount"
      :pageCount="pageCount"
      @getCurrentPage="getCurrentPage"
      @choosePage="choosePage"
    />
    </div>
</template>
<script setup lang="ts">
import {  ref } from 'vue'

import VuePithyCalendar from 'vue-pithy-calendar'
const allCount = ref(101);
const pageCount = ref(10)
const getCurrentPage = (currentPage: number) => {
  console.log(currentPage);
}
const choosePage = (count: number) => {
  pageCount.value = count
}
</script>
```
|      方法      | 是否必写 |       说明       | 返回结果 |
| :------------: | :------: | :--------------: | :------: |
| getCurrentPage |    是    | 获取点击的当前页 |  Number  |
|   choosePage   |    是    |  获取改变的页码  |  Number  |

|   参数    | 是否必传 |   说明   |  类型  |
| :-------: | :------: | :------: | :----: |
| allCount  |    是    |  总条数  | Number |
| pageCount |    是    | 每页条数 | Number |

效果：

![](https://i.loli.net/2021/05/11/verO7DzT9ocdKZa.png)