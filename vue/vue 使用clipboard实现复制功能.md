### vue 使用clipboard实现复制功能

在vue中使用clipboard.js 时候发现一个问题，如果移动端不是input或者button，则复制不成功，使用步骤如下

1.引入clipboard.js

```js
npm install clipboard --save	
```

2.在需要使用的组件中import

```js
import Clipboard from 'clipboard';		
```

3.添加需要复制的内容

```js
<button class="tag-read" data-clipboard-text="我是可以复制的内容，啦啦啦啦" @click="copy">立即阅读</button>	
```

4.

```js

copy() {
        var clipboard = new Clipboard('.tag-read')
        clipboard.on('success', e => {
          console.log('复制成功')
          // 释放内存
          clipboard.destroy()
        })
        clipboard.on('error', e => {
          // 不支持复制
          console.log('该浏览器不支持自动复制')
          // 释放内存
          clipboard.destroy()
        })
      }
```

或者

3.动态获取需要复制的内容

```html
<input type="text" v-model="copyContent"  id="copy_text" style="opacity: 0">
<button ref="copy"  data-clipboard-action="copy" data-clipboard-target="#copy_text" @click="copy">复制</button>
```

4.复制

```js
this.copyBtn = new this.$clipboard(this.$refs.copy)
```

```js
 copy () {
      let _this = this
      let clipboard = _this.copyBtn
      clipboard.on('success', function () {
        Toast('复制成功')
      })
      clipboard.on('error', function () {
        Toast('复制失败，请手动复制')
      })
    }
```

原文链接：[https://blog.csdn.net/guxuehua/article/details/79169190](https://blog.csdn.net/guxuehua/article/details/79169190)

