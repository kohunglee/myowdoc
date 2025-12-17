
- **Class 的本质**：是把“数据”和“操作数据的方法”绑定在一起。
- **替代方案**：你完全可以用“闭包”、“模块（Module）”或者单纯的“对象”来实现同样的效果。

**只要你的代码不是散落在地上的散沙，而是打包好的沙袋，用不用 Class 无所谓。**

#### 给核心加把锁（防手贱）

为了防止你或者别人的代码不小心写了 k.core = null 导致整个引擎崩溃，你可以使用 Object.freeze 或者 Object.defineProperty。

codeJavaScript

```
// 在引擎初始化最开始
window.k = {};
const coreSystem = { ... };

// 定义一个只读属性 'core'
Object.defineProperty(window.k, 'core', {
    value: coreSystem,
    writable: false, // 禁止修改！
    configurable: false // 禁止删除！
});
```