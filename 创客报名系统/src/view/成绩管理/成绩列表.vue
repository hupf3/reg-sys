<template>
  <div>
    <div>
      <Button type="primary" size="default" style="margin-right: 5px" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加成绩列表" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="参加的赛场">
            <Input v-model="formItem.session" placeholder="请填写参加的赛场"></Input>
          </FormItem>
          <FormItem label="报名编号">
            <Input v-model="formItem.number" placeholder="请填写报名编号"></Input>
          </FormItem>
          <FormItem label="选手姓名">
            <Input v-model="formItem.sname" placeholder="请填写选手姓名"></Input>
          </FormItem>
          <FormItem label="选手身份证">
            <Input v-model="formItem.id" placeholder="请填写选手身份证"></Input>
          </FormItem>
          <FormItem label="指导老师姓名">
            <Input v-model="formItem.tname" placeholder="请填写指导老师姓名"></Input>
          </FormItem>
          <FormItem label="赛事类型">
            <Input v-model="formItem.type" placeholder="请填写赛事类型"></Input>
          </FormItem>
          <FormItem label="参赛单位">
            <Input v-model="formItem.work" placeholder="请填写参赛单位"></Input>
          </FormItem>
          <FormItem label="得分">
            <Input v-model="formItem.score" placeholder="请填写得分"></Input>
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
      <Modal v-model="modal2" title="编辑成绩列表" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="参加的赛场">
            <Input v-model="formItem.session" placeholder="请填写参加的赛场"></Input>
          </FormItem>
          <FormItem label="报名编号">
            <Input v-model="formItem.number" placeholder="请填写报名编号"></Input>
          </FormItem>
          <FormItem label="选手姓名">
            <Input v-model="formItem.sname" placeholder="请填写选手姓名"></Input>
          </FormItem>
          <FormItem label="选手身份证">
            <Input v-model="formItem.id" placeholder="请填写选手身份证"></Input>
          </FormItem>
          <FormItem label="指导老师姓名">
            <Input v-model="formItem.tname" placeholder="请填写指导老师姓名"></Input>
          </FormItem>
          <FormItem label="赛事类型">
            <Input v-model="formItem.type" placeholder="请填写赛事类型"></Input>
          </FormItem>
          <FormItem label="参赛单位">
            <Input v-model="formItem.work" placeholder="请填写参赛单位"></Input>
          </FormItem>
          <FormItem label="得分">
            <Input v-model="formItem.score" placeholder="请填写得分"></Input>
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
          session: '',
          number: '',
          sname: '',
          id: '',
          tname: '',
          type: '',
          work: '',
          score: ''
        },
        columns: [{
            type: 'selection',
            width: 60,
            align: 'center'
          },
          {
            title: '参加赛场',
            key: 'session'
          },
          {
            title: '报名编号',
            key: 'number'
          },
          {
            title: '选手姓名',
            key: 'sname'
          },
          {
            title: '选手身份证',
            key: 'id'
          },
          {
            title: '指导老师姓名',
            key: 'tname'
          },
          {
            title: '赛事类型',
            key: 'type'
          },
          {
            title: '参赛单位',
            key: 'work'
          },
          {
            title: '得分',
            key: 'score'
          },
          {
            title: '操作',
            width: 150,
            slot: 'edit'
          }
        ],
        datas: [{
          session: '上午',
          number: 1234,
          sname: '小王',
          id: 234,
          tname: '小白',
          type: '笔试',
          work: '东风小学',
          score: 98
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
        this.formItem.session = this.datas[index].session
        this.formItem.number = this.datas[index].number
        this.formItem.sname = this.datas[index].sname
        this.formItem.id = this.datas[index].id
        this.formItem.tname = this.datas[index].tname
        this.formItem.type = this.datas[index].type
        this.formItem.work = this.datas[index].work
        this.formItem.score = this.datas[index].score
        this.index_t = index
      },
      clear() {
        this.formItem = {
          session: '',
          number: '',
          sname: '',
          id: '',
          tname: '',
          type: '',
          work: '',
          score: ''
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
        this.datas[this.index_t].session = this.formItem.session
        this.datas[this.index_t].number = this.formItem.number
        this.datas[this.index_t].sname = this.formItem.sname
        this.datas[this.index_t].id = this.formItem.id
        this.datas[this.index_t].tname = this.formItem.tname
        this.datas[this.index_t].type = this.formItem.type
        this.datas[this.index_t].work = this.formItem.work
        this.datas[this.index_t].score = this.formItem.score
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
