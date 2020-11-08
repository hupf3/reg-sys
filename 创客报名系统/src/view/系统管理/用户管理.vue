<template>
  <div>
    <div>
      <Select v-model="searchKey" style="width: 200px;">
        <Option v-for="item in columns" v-if="item.title !== '操作' && item.type != 'selection'" :value="item.key" :key="`search-col-${item.key}`">{{ item.title }}</Option>
      </Select>
      <Input @on-change="handleClear" clearable placeholder="输入关键字搜索" style="width: 200px" v-model="searchValue"></Input>
      {{" "}}
      <Button @click="handleSearch" type="primary">搜索</Button>
      {{" "}}
      <Button type="success" size="default" style="margin-right: 5px;" @click="modal1=true">添加</Button>
      <Modal v-model="modal1" title="添加用户数据" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="用户ID">
            <Input v-model="formItem.id" placeholder="请填写用户ID"></Input>
          </FormItem>
          <FormItem label="用户类型">
            <RadioGroup v-model="formItem.type">
              <Radio label="系统管理员"></Radio>
              <Radio label="公众号用户"></Radio>
            </RadioGroup>
            <!-- <Input v-model="formItem.type" placeholder="请填写用户类型"></Input> -->
          </FormItem>
          <FormItem label="用户账户">
            <Input v-model="formItem.account" placeholder="请填写用户账户"></Input>
          </FormItem>
          <FormItem label="用户密码">
            <Input v-model="formItem.password" placeholder="请填写用户密码"></Input>
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
      <Modal v-model="modal2" title="编辑用户数据" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="用户ID">
            <Input v-model="formItem.id" placeholder="请填写用户ID"></Input>
          </FormItem>
          <FormItem label="用户类型">
            <RadioGroup v-model="formItem.type">
              <Radio label="系统管理员"></Radio>
              <Radio label="公众号用户"></Radio>
            </RadioGroup>
            <!-- <Input v-model="formItem.type" placeholder="请填写用户类型"></Input> -->
          </FormItem>
          <FormItem label="用户账户">
            <Input v-model="formItem.account" placeholder="请填写用户账户"></Input>
          </FormItem>
          <FormItem label="用户密码">
            <Input v-model="formItem.password" placeholder="请填写用户密码"></Input>
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
        searchValue: '',
        searchKey: '',
        formItem: {
          id: '',
          type: '',
          account: '',
          password: ''
        },
        columns: [{
            type: 'selection',
            width: 60,
            align: 'center'
          },
          {
            title: '用户ID',
            key: 'id'
          },
          {
            title: '用户类型',
            key: 'type'
          },
          {
            title: '用户账户',
            key: 'account'
          },
          {
            title: '用户密码',
            key: 'password'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          id: '8435656',
          type: '系统管理员',
          account: 'hupf3',
          password: '123456'
        }],
        datas_t: []
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
          id: '',
          type: '',
          account: '',
          password: ''
        }
        this.index_t = -1
      },
      modify(index) {
        this.modal2 = true
        this.formItem.id = this.datas[index].id
        this.formItem.type = this.datas[index].type
        this.formItem.account = this.datas[index].account
        this.formItem.password = this.datas[index].password
        this.index_t = index
      },
      ok1() {
        this.$Message.info('添加成功！')
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
        this.datas[this.index_t].type = this.formItem.type
        this.datas[this.index_t].account = this.formItem.account
        this.datas[this.index_t].password = this.formItem.password
        this.clear()
        this.modal2 = false
      },
      cancel2() {
        this.$Message.info('取消编辑！')
        this.clear()
        this.modal2 = false
      },
      handleClear(e) {
        if (e.target.value === '') this.datas = this.datas_t
      },
      handleSearch() {
        this.datas_t = this.datas
        this.datas = this.datas_t.filter(item => item[this.searchKey].indexOf(this.searchValue) > -1)
      }
    }
  }
</script>
