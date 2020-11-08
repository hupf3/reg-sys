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
      <Modal v-model="modal1" title="添加赛事动态" @on-ok="ok1" @on-cancel="cancel1">
        <Form :model="formItem" :label-width="100">
          <FormItem label="标题">
            <Input v-model="formItem.heading" placeholder="请填写标题"></Input>
          </FormItem>
          <FormItem label="内容">
            <markdown-editor v-model="formItem.content" />
            <!-- <Input v-model="formItem.content" placeholder="请填写内容"></Input> -->
          </FormItem>
          <FormItem label="发布时间">
            <Input v-model="formItem.rtime" placeholder="请填写发布时间"></Input>
          </FormItem>
          <FormItem label="修改时间">
            <Input v-model="formItem.ctime" placeholder="请填写修改时间"></Input>
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
      <Modal v-model="modal2" title="编辑赛事动态" @on-ok="ok2" @on-cancel="cancel2">
        <Form :model="formItem" :label-width="100">
          <FormItem label="标题">
            <Input v-model="formItem.heading" placeholder="请填写标题"></Input>
          </FormItem>
          <FormItem label="内容">
            <markdown-editor v-model="formItem.content" />
            <!-- <Input v-model="formItem.content" placeholder="请填写内容"></Input> -->
          </FormItem>
          <FormItem label="发布时间">
            <Input v-model="formItem.rtime" placeholder="请填写发布时间"></Input>
          </FormItem>
          <FormItem label="修改时间">
            <Input v-model="formItem.ctime" placeholder="请填写修改时间"></Input>
          </FormItem>
        </Form>
      </Modal>
    </div>
  </div>
</template>
<script>
  import MarkdownEditor from '_c/markdown'
  export default {
    components: {
      MarkdownEditor
    },
    data() {
      return {
        modal1: false,
        modal2: false,
        index_t: -1,
        searchValue: '',
        searchKey: '',
        formItem: {
          heading: '',
          content: '',
          rtime: '',
          ctime: ''
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
            title: '内容',
            key: 'content'
          },
          {
            title: '发布时间',
            key: 'rtime'
          },
          {
            title: '修改时间',
            key: 'ctime'
          },
          {
            title: '操作',
            slot: 'edit'
          }
        ],
        datas: [{
          heading: '康磊杯',
          content: '赛事成功举办',
          rtime: '2020.10.12',
          ctime: '2020.10.23'
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
      modify(index) {
        this.modal2 = true
        this.formItem.content = this.datas[index].content
        this.formItem.heading = this.datas[index].heading
        this.formItem.ctime = this.datas[index].ctime
        this.formItem.rtime = this.datas[index].rtime
        this.index_t = index
      },
      clear() {
        this.formItem = {
          heading: '',
          content: '',
          rtime: '',
          ctime: ''
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
        this.datas[this.index_t].heading = this.formItem.heading
        this.datas[this.index_t].ctime = this.formItem.ctime
        this.datas[this.index_t].rtime = this.formItem.rtime
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
