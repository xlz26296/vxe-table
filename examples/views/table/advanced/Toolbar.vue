<template>
  <div>
    <p>使用自带的工具栏 <toolbar-api-link name="vxe-toolbar"/>，配合模板可以非常简单的实现强大的功能</p>
    <p>支持显示/隐藏列、列宽拖动状态的保存功能</p>
    <p class="red">组成一套完整的表格，工具栏和表格必须是上下相邻关系，渲染时会自动进行上下关联，不允许更换位置（如果是复杂的布局不建议使用工具栏，自行写模板即可）</p>

    <vxe-toolbar setting :refresh="{query: findList}">
      <template v-slot:buttons>
        <vxe-button>{{ $t('app.body.button.insert') }}</vxe-button>
        <vxe-button>按钮2</vxe-button>
      </template>
    </vxe-toolbar>

    <vxe-table
      border
      height="400"
      :loading="loading"
      :data.sync="tableData">
      <vxe-table-column type="index" width="60"></vxe-table-column>
      <vxe-table-column field="name" title="app.body.label.name"></vxe-table-column>
      <vxe-table-column field="role" title="Role"></vxe-table-column>
      <vxe-table-column field="sex" title="app.body.label.sex"></vxe-table-column>
      <vxe-table-column field="age" title="app.body.label.age"></vxe-table-column>
      <vxe-table-column field="rate" title="Rate"></vxe-table-column>
    </vxe-table>

    <p class="demo-code">{{ $t('app.body.button.showCode') }}</p>

    <pre>
      <code class="xml">{{ demoCodes[0] }}</code>
      <code class="javascript">{{ demoCodes[1] }}</code>
    </pre>
  </div>
</template>

<script>
import hljs from 'highlight.js'

export default {
  data () {
    return {
      loading: false,
      tableData: [],
      demoCodes: [
        `
        <vxe-toolbar setting :refresh="{query: findList}">
          <template v-slot:buttons>
            <vxe-button>{{ $t('app.body.button.insert') }}</vxe-button>
            <vxe-button>按钮2</vxe-button>
          </template>
        </vxe-toolbar>

        <vxe-table
          border
          height="400"
          :loading="loading"
          :data.sync="tableData">
          <vxe-table-column type="index" width="60"></vxe-table-column>
          <vxe-table-column field="name" title="app.body.label.name"></vxe-table-column>
          <vxe-table-column field="role" title="Role"></vxe-table-column>
          <vxe-table-column field="sex" title="app.body.label.sex"></vxe-table-column>
          <vxe-table-column field="age" title="app.body.label.age"></vxe-table-column>
          <vxe-table-column field="rate" title="Rate"></vxe-table-column>
        </vxe-table>
        `,
        `
        export default {
          data () {
            return {
              loading: false,
              tableData: []
            }
          },
          created () {
            this.findList()
          },
          methods: {
            findList () {
              this.loading = true
              return new Promise(resolve => {
                setTimeout(() => {
                  this.tableData = window.MOCK_DATA_LIST.slice(0, 20)
                  this.loading = false
                  resolve()
                }, 300)
              })
            }
          }
        }
        `
      ]
    }
  },
  created () {
    this.findList()
  },
  mounted () {
    Array.from(this.$el.querySelectorAll('pre code')).forEach((block) => {
      hljs.highlightBlock(block)
    })
  },
  methods: {
    findList () {
      this.loading = true
      return new Promise(resolve => {
        setTimeout(() => {
          this.tableData = window.MOCK_DATA_LIST.slice(0, 20)
          this.loading = false
          resolve()
        }, 300)
      })
    }
  }
}
</script>
