# Clock

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```
>从这里进去可以看到项目效果：https://rrbetsy.github.io/Clock/.

本项目是由 vue-cli 创建的
时钟分解为两部分：钟面和时针。
钟面又分为外圈、刻度和里面的数字，时针部分包括最里面的中心点和时针、分针、秒针。
**外圈、刻度和数字的对应关系**
外圈是360度，刻度一共有60个，一个刻度为6度，长刻度有12个，对应1~12的数字，刚好是5的倍数，数字可以表示为 `n%5==0` ，样式则写为`:nth-child(5n-1)`。
>因为 `v-for` 指令里面的`n in 60` 是表示 1~60 的数字，参数 `5n-1` 里面的 n 是从 0 开始的，所有需要减去 1 ）。

**中心点**用css3属性 `box-shadow` 设置，可以设置多层阴影。（本身颜色是黄色，内阴影青绿色，最外层是红色）
```
box-shadow: 0 0 0 5px #c0ee0a inset, 0 0 0 5px #ee0a15;
```
**秒针、分针、时针和角度之间的对应关系**
秒针：一圈 360 度，转一圈 60s，1s 就是 6 度，刚好是一刻度，所以秒针的角度`secondsRotate = seconds * 6`。
分针：分针转一圈是 60m，等于 3600s，1m 就是 6 度。秒针转完一圈 60s，分针就转 1m。但是当秒针还没转完一圈时，分针、时针也是在转的，比如当秒针第一圈转到 180 度时，分针应该也转了 3 度。所以分针的角度`minutesRotate = minutes * 6 + secondsRotate/60`。

