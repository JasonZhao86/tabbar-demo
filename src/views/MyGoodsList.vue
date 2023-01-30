<template>
  <div>
    <MyTable :arr="goodsList">
      <!-- 具名插槽 -->
      <template #header>
        <th>#</th>
        <th>商品名称</th>
        <th>价格</th>
        <th>标签</th>
        <th>操作</th>
      </template>
      <!-- 作用域插槽 -->
      <template #body="scope">
        <td>{{ scope.row.id }}</td>
        <td>{{ scope.row.goods_name }}</td>
        <td>￥ {{ scope.row.goods_price }}</td>
        <td>
          <input
            class="tag-input form-control"
            style="witdh: 100px"
            type="text"
            v-if="scope.row.inputVisible"
            v-focus
            @blur="scope.row.inputVisible = false"
            v-model="scope.row.inputValue"
            @keydown.enter="enterFn(scope.row)"
            @keydown.esc="scope.row.inputValue = ''"
          />
          <button
            v-else
            style="display: block"
            class="btn btn-primary btn-sm add-tag"
            @click="scope.row.inputVisible = true"
          >
            +Tag
          </button>
          <span
            v-for="(item, index) in scope.row.tags"
            :key="index"
            class="badge text-bg-warning"
          >
            {{ item }}
          </span>
        </td>
        <td>
          <!-- scope的值: {row: obj, index: 索引值} -->
          <button class="btn btn-danger btn-sm" @click="removeBtn(scope.index)">
            删除
          </button>
        </td>
      </template>
    </MyTable>
  </div>
</template>

<script>
import MyTable from '@/components/MyTable'
export default {
  name: 'MyGoodsList',
  components: {
    MyTable,
  },
  data() {
    return {
      goodsList: [],
    }
  },
  created() {
    this.$axios({
      url: '/api/goods',
    })
      .then((res) => {
        console.log(res.data.data)
        this.goodsList = res.data.data
      })
      .catch((err) => console.error(err))
  },
  methods: {
    removeBtn(index) {
      this.goodsList.splice(index, 1)
    },
    enterFn(obj) {
      if (!obj.inputValue.trim()) {
        alert('请输入数据')
        return
      }
      obj.tags.push(obj.inputValue)
      obj.inputValue = ''
    },
  },
}
</script>

<style lang="less" scoped>
.my-goods-list {
  .badge {
    margin-right: 5px;
  }
}
</style>
