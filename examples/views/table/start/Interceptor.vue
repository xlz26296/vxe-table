<template>
  <div>
    <h2>Event collision interceptor 事件冲突拦截器</h2>
    <p>通过内置拦截器可以解决当表格的事件处理与第三方组件存在冲突的问题，从而可以集成其他组件互相兼容；比如这些插件 <a class="link" href="https://www.npmjs.com/package/vxe-table-plugin-element" target="_blank">vxe-table-plugin-element</a></p>
    <h3>API</h3>
    <p class="green">添加一个拦截器 interceptor.add(type, callback)</p>
    <h3>type 可选值</h3>
    <p class="orange">event.clear_filter（清除筛选面板时触发）</p>
    <p class="orange">event.clear_actived（清除激活单元格时触发）</p>
    <p>例子：比如自定义渲染某个组件后，由于弹出层面板不在单元格之内，按键事件的交互行为存在冲突，对于这些场景就很有用了</p>
    <pre>
      <code class="javascript">{{ demoCodes[0] }}</code>
    </pre>
  </div>
</template>

<script>
import hljs from 'highlight.js'

export default {
  data () {
    return {
      demoCodes: [
        `
        VXETable.interceptor.add('event.clear_actived', (params, event) => {
          // 比如点击了某个组件的弹出层面板之后，此时被激活单元格不应该被自动关闭，通过返回 false 可以阻止默认的行为。
          if (event.target.className.indexOf('other-popper') > -1) {
            return false
          }
        })
        `
      ]
    }
  },
  mounted () {
    Array.from(this.$el.querySelectorAll('pre code')).forEach((block) => {
      hljs.highlightBlock(block)
    })
  }
}
</script>
