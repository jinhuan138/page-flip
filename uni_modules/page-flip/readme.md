# page-flip

### 使用说明

```vue
<template>
<view style="height: 80%; width: 80%;">
    <page-flip :papers="papers" @pageChange="pageChange"/>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                papers: [],
            };
        },
        mounted() {
            const baseurl = "https://raw.githubusercontent.com/jinhuan138/page-flip/main/static/新人教初中七下生物(2022版课标修订)-图片";
            for (let i = 0; i <= 10; i++) {
                this.papers.push(`${baseurl}-${i}.jpg`);
            }
        },
        methods: {
            pageChange(page) {
                console.log("当前页码", page);
            },
        },
    };
</script>
```


### 属性
| **属性名** | **说明** | **类型** | **默认值** |
| ---------- | -------- | ---------|----------- |
| papers     | 图片地址 |   Array    | [] |

### 事件
| **事件名** | **说明**   | **Type**                       |
| ---------- | ---------- | ------------------------------ |
| pageChange | 翻页时触发 | (value: page) => void |

