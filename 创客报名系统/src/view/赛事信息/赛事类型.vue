<template>
  <div>
    <div>
      <Button type="primary" size="default" style="margin-right: 5px" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加赛事类型" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="赛事名称">
            <Input v-model="formItem.name" placeholder="请填写赛事名称"></Input>
          </FormItem>
          <FormItem label="赛事类型">
            <Input v-model="formItem.type" placeholder="请填写赛事类型"></Input>
          </FormItem>
          <FormItem label="类型说明">
            <Input v-model="formItem.description" placeholder="请填写类型说明"></Input>
          </FormItem>
        </Form>
      </Modal>
    </div>
    <br />
    <div>
      <Table border :columns="columns" :data="datas">
        <template slot-scope="{ row, index }" slot="edit">
          <Button type="error" size="small" @click="remove(index)">删除</Button>
          {{" "}}
          <Button type="primary" size="small" @click="modify(index)">编辑</Button>
        </template>
      </Table>
      <Modal v-model="modal2" title="编辑赛事类型" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="赛事名称">
            <Input v-model="formItem.name" placeholder="请填写赛事名称"></Input>
          </FormItem>
          <FormItem label="赛事类型">
            <Input v-model="formItem.type" placeholder="请填写赛事类型"></Input>
          </FormItem>
          <FormItem label="类型说明">
            <Input v-model="formItem.description" placeholder="请填写类型说明"></Input>
          </FormItem>
        </Form>
      </Modal>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        modal1: false,
        modal2: false,
        index_t: -1,
        formItem: {
          name: '',
          type: '',
          description: ''
        },
        columns: [{
            type: 'selection',
            width: 60,
            align: 'center'
          },
          {
            title: '赛事名称',
            key: 'name'
          },
          {
            title: '赛事类型',
            key: 'type'
          },
          {
            title: '类型说明',
            key: 'description'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          name: '康乐杯',
          type: '小学组',
          description: '编程'
        }]
      }
    },
    methods: {
      remove(index) {
        this.datas.splice(index, 1)
      },
      add(obj) {
        this.datas.push(obj)
      },
      clear() {
        this.formItem = {
          name: '',
          type: '',
          description: ''
        }
        this.index_t = -1
      },
      modify(index) {
        this.modal2 = true
        this.formItem.name = this.datas[index].name
        this.formItem.type = this.datas[index].type
        this.formItem.description = this.datas[index].description
        this.index_t = index
      },
      ok1() {
        this.$Message.info('成功添加！')
        this.add(this.formItem)
        this.clear()
        this.modal1 = false
      },
      cancel1() {
        this.$Message.info('取消添加！')
        this.modal1 = false
        this.clear()
      },
      ok2() {
        this.$Message.info('编辑成功！')
        this.datas[this.index_t].name = this.formItem.name
        this.datas[this.index_t].type = this.formItem.type
        this.datas[this.index_t].description = this.formItem.description
        this.clear()
        this.modal2 = false
      },
      cancel2() {
        this.$Message.info('取消编辑！')
        this.clear()
        this.modal2 = false
      }
    }
  }
</script>
