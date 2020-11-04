<template>
  <div>
    <div>
      <Button type="primary" size="default" style="margin-right: 5px" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加赛场信息" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="赛事名称">
            <Input v-model="formItem.name" placeholder="请填写赛事名称"></Input>
          </FormItem>
          <FormItem label="报名截止">
            <Input v-model="formItem.deadline" placeholder="请填写报名截止"></Input>
          </FormItem>
          <FormItem label="赛场">
            <Input v-model="formItem.place" placeholder="请填写赛场"></Input>
          </FormItem>
          <FormItem label="比赛日期">
            <Input v-model="formItem.time" placeholder="请填写比赛日期"></Input>
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
      <Modal v-model="modal2" title="编辑赛场信息" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="赛事名称">
            <Input v-model="formItem.name" placeholder="请填写赛事名称"></Input>
          </FormItem>
          <FormItem label="报名截止">
            <Input v-model="formItem.deadline" placeholder="请填写报名截止"></Input>
          </FormItem>
          <FormItem label="赛场">
            <Input v-model="formItem.place" placeholder="请填写赛场"></Input>
          </FormItem>
          <FormItem label="比赛日期">
            <Input v-model="formItem.time" placeholder="请填写比赛日期"></Input>
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
          deadline: '',
          place: '',
          time: ''
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
            title: '报名截止',
            key: 'deadline'
          },
          {
            title: '赛场(省/市)',
            key: 'place'
          },
          {
            title: '比赛日期',
            key: 'time'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          name: '康乐杯',
          deadline: '2020 - 10 - 23',
          place: '广东省广州市',
          time: '2020 - 10 - 30'
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
        this.formItem.name = this.datas[index].name
        this.formItem.deadline = this.datas[index].deadline
        this.formItem.place = this.datas[index].place
        this.formItem.time = this.datas[index].time
        this.index_t = index
      },
      clear() {
        this.formItem = {
          name: '',
          deadline: '',
          place: '',
          time: ''
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
        this.clear()
        this.modal1 = false
      },
      ok2() {
        this.$Message.info('编辑成功！')
        this.datas[this.index_t].name = this.formItem.name
        this.datas[this.index_t].deadline = this.formItem.deadline
        this.datas[this.index_t].place = this.formItem.place
        this.datas[this.index_t].time = this.formItem.time
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
