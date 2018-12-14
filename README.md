## vue week 组件
网上没有vue的选择一个星期的组件 就自己写了一个简单的
[![FUP6l6.md.png](https://s1.ax1x.com/2018/12/14/FUP6l6.md.png)](https://imgchr.com/i/FUP6l6)

# 功能
  * 选择上一周下一周
  * 展示一周星期和日期
  * 默认当天背景为红色 便于区分
  * 单击时间 返回当天

# 使用方法
```javascript
import Date from "XX/date.vue";

export default {
  name: "Cygl",
  props: ["currentTreenode"],
  components: {
    Date
 }
 <Date></Date>
 ```
