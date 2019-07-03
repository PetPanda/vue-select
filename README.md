# vue-select
VUE Select component
## 使用方法：
1. 引入组件:

```javascript
import VueSelect from '../components/VueSelect'
```

2. 注册组件

```javscript
export default {
    components: {
        VueSelect
    }
}
```

3. 使用组件

```html
<template>
    <vue-select
     :options="options"
     name="name"
     value="id"
     placeholder="请选择类型"
     v-model="selected_id"
     @change="handleChange">
    </vue-select>
</template>
```

`options`：选择项列表；

`name`：选择项列表中选择项名称的属性名；

`value`：选择项列表中选择项的值的属性名；

`v-model`：对应双向绑定的选中后的值；

`@change`：选择发生改变后触发事件，回调参数：当前选项。

## DEMO:

```html
<template>
    <div>
         <vue-select
        :options="options"
        name="name"
        value="id"
        placeholder="请选择一个水果"
        v-model="selected_id"
        @change="handleChange">
        </vue-select>
    </div>
</template>

<script>
import VueSelect from '../components/VueSelect'
export default {
    name: "Index",
    data() {
        return {
            selected_id: "",
            options: [
                {name: "苹果", id: 1},
                {name: "橘子", id: 2},
                {name: "香蕉", id: 3},
                {name: "西瓜", id: 4},
            ]
        }
    },
    components: {
        VueSelect
    },
    methods: {
        handleChange(e) {
            console.log(e)
        }
    }
}
</script>
```