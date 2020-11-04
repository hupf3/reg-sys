<template>
  <div>
    <div>
      <Button type="primary" size="default" style="margin-right: 5px" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加报名列表" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="报名编号">
            <Input v-model="formItem.id" placeholder="请填写报名编号"></Input>
          </FormItem>
          <FormItem label="选手姓名">
            <Input v-model="formItem.sname" placeholder="请填写选手姓名"></Input>
          </FormItem>
          <FormItem label="指导老师姓名">
            <Input v-model="formItem.tname" placeholder="请填写指导老师姓名"></Input>
          </FormItem>
          <FormItem label="参赛单位">
            <Input v-model="formItem.work" placeholder="请填写参赛单位"></Input>
          </FormItem>
          <FormItem label="参加的赛区">
            <Input v-model="formItem.place" placeholder="请填写参加的赛区"></Input>
          </FormItem>
          <FormItem label="报名时间">
            <Input v-model="formItem.time" placeholder="请填写报名时间"></Input>
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
      <Modal v-model="modal2" title="编辑报名列表" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="报名编号">
            <Input v-model="formItem.id" placeholder="请填写报名编号"></Input>
          </FormItem>
          <FormItem label="选手姓名">
            <Input v-model="formItem.sname" placeholder="请填写选手姓名"></Input>
          </FormItem>
          <FormItem label="指导老师姓名">
            <Input v-model="formItem.tname" placeholder="请填写指导老师姓名"></Input>
          </FormItem>
          <FormItem label="参赛单位">
            <Input v-model="formItem.work" placeholder="请填写参赛单位"></Input>
          </FormItem>
          <FormItem label="参加的赛区">
            <Input v-model="formItem.place" placeholder="请填写参加的赛区"></Input>
          </FormItem>
          <FormItem label="报名时间">
            <Input v-model="formItem.time" placeholder="请填写报名时间"></Input>
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
          id: '',
          sname: '',
          tname: '',
          work: '',
          place: '',
          time: ''
        },
        columns: [{
            type: 'selection',
            width: 60,
            align: 'center'
          },
          {
            title: '报名编号',
            key: 'id'
          },
          {
            title: '选手姓名',
            key: 'sname'
          },
          {
            title: '指导老师姓名',
            key: 'tname'
          },
          {
            title: '参赛单位',
            key: 'work'
          },
          {
            title: '参加的赛区',
            key: 'place'
          },
          {
            title: '报名时间',
            key: 'time'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          id: 2014,
          sname: '小王',
          tname: '小红',
          work: '东风小学',
          place: '华南赛区',
          time: '2019 - 02 - 17'
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
        this.formItem.id = this.datas[index].id
        this.formItem.sname = this.datas[index].sname
        this.formItem.tname = this.datas[index].tname
        this.formItem.work = this.datas[index].work
        this.formItem.place = this.datas[index].place
        this.formItem.time = this.datas[index].time
        this.index_t = index
      },
      clear() {
        this.formItem = {
          id: '',
          sname: '',
          tname: '',
          work: '',
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
        this.modal1 = false
        this.clear()
      },
      ok2() {
        this.$Message.info('编辑成功！')
        this.datas[this.index_t].id = this.formItem.id
        this.datas[this.index_t].sname = this.formItem.sname
        this.datas[this.index_t].tname = this.formItem.tname
        this.datas[this.index_t].work = this.formItem.work
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
