```js
import { initMixin } from "./init";
import { stateMixin } from "./state";
import { renderMixin } from "./render";
import { eventsMixin } from "./events";
import { lifecycleMixin } from "./lifecycle";
import { warn } from "../util/index";

function Vue(options) {
  if (process.env.NODE_ENV !== "production" && !(this instanceof Vue)) {
    warn("Vue is a constructor and should be called with the `new` keyword");
  }
  this._init(options);
}

initMixin(Vue);
stateMixin(Vue);
eventsMixin(Vue);
lifecycleMixin(Vue);
renderMixin(Vue);

export default Vue;
```

- process.env.NODE_ENV !== "production" && !(this instanceof Vue)<br>
  指 Vue 项目的生产环境必须使用 new 调用 Vue 构造函数。生产环境指的是 Vue 项目，而不是开发者基于 Vue 的项目。
  <br>
- .init 应该是挂载到了 Vue 的原型上。
-
