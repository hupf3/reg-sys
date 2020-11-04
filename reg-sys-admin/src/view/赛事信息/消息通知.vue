<template>
  <div>
    <div>
      <Button type="primary" size="default" style="margin-right: 5px" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加消息通知" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="标题">
            <Input v-model="formItem.heading" placeholder="请填写标题"></Input>
          </FormItem>
          <FormItem label="发布时间">
            <Input v-model="formItem.time" placeholder="请填写输入时间"></Input>
          </FormItem>
          <FormItem label="类型">
            <Input v-model="formItem.type" placeholder="请填写类型"></Input>
          </FormItem>
          <FormItem label="赛事内容">
            <Input v-model="formItem.content" placeholder="请填写赛事内容"></Input>
          </FormItem>
          <FormItem label="地址">
            <Input v-model="formItem.address" placeholder="请填写地址"></Input>
          </FormItem>
          <FormItem label="电话">
            <Input v-model="formItem.phone" placeholder="请填写电话"></Input>
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
      <Modal v-model="modal2" title="编辑消息通知" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="标题">
            <Input v-model="formItem.heading" placeholder="请填写标题"></Input>
          </FormItem>
          <FormItem label="发布时间">
            <Input v-model="formItem.time" placeholder="请填写输入时间"></Input>
          </FormItem>
          <FormItem label="类型">
            <Input v-model="formItem.type" placeholder="请填写类型"></Input>
          </FormItem>
          <FormItem label="赛事内容">
            <Input v-model="formItem.content" placeholder="请填写赛事内容"></Input>
          </FormItem>
          <FormItem label="地址">
            <Input v-model="formItem.address" placeholder="请填写地址"></Input>
          </FormItem>
          <FormItem label="电话">
            <Input v-model="formItem.phone" placeholder="请填写电话"></Input>
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
          heading: '',
          time: '',
          type: '',
          content: '',
          address: '',
          phone: ''
        },
        columns: [{
            type: 'selection',
            width: 60,
            align: 'center'
          },
          {
            title: '标题',
            key: 'heading'
          },
          {
            title: '发布时间',
            key: 'time'
          },
          {
            title: '类型',
            key: 'type'
          },
          {
            title: '赛事内容',
            key: 'content'
          },
          {
            title: '地址',
            key: 'address'
          },
          {
            title: '电话',
            key: 'phone'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          heading: '头条',
          time: '2020 - 10 - 23',
          type: '平台',
          content: '康乐杯举办',
          address: '中山大学东校区',
          phone: '60080'
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
        this.formItem.heading = this.datas[index].heading
        this.formItem.type = this.datas[index].type
        this.formItem.time = this.datas[index].time
        this.formItem.content = this.datas[index].content
        this.formItem.address = this.datas[index].address
        this.formItem.phone = this.datas[index].phone
        this.index_t = index
      },
      clear() {
        this.formItem = {
          heading: '',
          time: '',
          type: '',
          content: '',
          address: '',
          phone: ''
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
        this.datas[this.index_t].heading = this.formItem.heading
        this.datas[this.index_t].type = this.formItem.type
        this.datas[this.index_t].time = this.formItem.time
        this.datas[this.index_t].content = this.formItem.content
        this.datas[this.index_t].address = this.formItem.address
        this.datas[this.index_t].phone = this.formItem.phone
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
