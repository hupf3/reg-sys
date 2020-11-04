<template>
  <div>
    <div>
      <Button type="primary" size="default" style="margin-right: 5px" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加赛事简介" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="赛事内容">
            <Input v-model="formItem.content" placeholder="请填写赛事内容"></Input>
          </FormItem>
          <FormItem label="赛事ID">
            <Input v-model="formItem.id" placeholder="请填写赛事ID"></Input>
          </FormItem>
          <FormItem label="有效时间">
            <Input v-model="formItem.etime" placeholder="请填写有效时间"></Input>
          </FormItem>
          <FormItem label="发布时间">
            <Input v-model="formItem.rtime" placeholder="请填写发布时间"></Input>
          </FormItem>
          <FormItem label="发布状态">
            <Input v-model="formItem.state" placeholder="请填写发布状态"></Input>
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
      <Modal v-model="modal2" title="编辑赛事简介" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="赛事内容">
            <Input v-model="formItem.content" placeholder="请填写赛事内容"></Input>
          </FormItem>
          <FormItem label="赛事ID">
            <Input v-model="formItem.id" placeholder="请填写赛事ID"></Input>
          </FormItem>
          <FormItem label="有效时间">
            <Input v-model="formItem.etime" placeholder="请填写有效时间"></Input>
          </FormItem>
          <FormItem label="发布时间">
            <Input v-model="formItem.rtime" placeholder="请填写发布时间"></Input>
          </FormItem>
          <FormItem label="发布状态">
            <Input v-model="formItem.state" placeholder="请填写发布状态"></Input>
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
          content: '',
          id: '',
          etime: '',
          rtime: '',
          state: ''
        },
        columns: [{
            type: 'selection',
            width: 60,
            align: 'center'
          },
          {
            title: '赛事内容',
            key: 'content'
          },
          {
            title: '赛事ID',
            key: 'id'
          },
          {
            title: '有效时间',
            key: 'etime'
          },
          {
            title: '发布时间',
            key: 'rtime'
          },
          {
            title: '发布状态',
            key: 'state'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          content: '康乐杯',
          id: '123',
          etime: '2019 - 10 - 23 -- 2019 - 10 - 25',
          rtime: '2019 - 10 - 19',
          state: '已发布'
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
      modify(index) {
        this.modal2 = true
        this.formItem.content = this.datas[index].content
        this.formItem.id = this.datas[index].id
        this.formItem.etime = this.datas[index].etime
        this.formItem.rtime = this.datas[index].rtime
        this.formItem.state = this.datas[index].state
        this.index_t = index
      },
      clear() {
        this.formItem = {
          content: '',
          id: '',
          etime: '',
          rtime: '',
          state: ''
        }
        this.index_t = -1
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
        this.datas[this.index_t].content = this.formItem.content
        this.datas[this.index_t].id = this.formItem.id
        this.datas[this.index_t].etime = this.formItem.etime
        this.datas[this.index_t].rtime = this.formItem.rtime
        this.datas[this.index_t].state = this.formItem.state
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
