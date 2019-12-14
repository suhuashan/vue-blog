<template>
    <el-form :model="form">
        <el-form-item class="main-container" v-for="(item, index) in form.list" :key="keyList[index]"
                      :prop="'list.' + index + '.value'"
                      :rules="{
                        validator: validateName, trigger: 'blur'
                       }">
            <el-input class="main-input" v-model="item.value"></el-input>
            <el-button v-if="index === form.list.length -1" @click="add(index)">+</el-button>
            <el-button v-if="form.list.length > 1" @click="sub(index)">-</el-button>
      </el-form-item>
    </el-form>
</template>

<script>

export default {
  name: 'SKey',
  data () {
    var validateName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('输入不能为空'))
      } else {
        if (value.length > 5) {
          callback(new Error('输入项不能超过5个字符'))
        }
      }
    }
    return {
      form: {
        list: [
          {
            value: ''
          }
        ]
      },
      keyList: [this.uuid(0)],
      validateName
    }
  },
  methods: {
    add (index) {
      this.keyList.push(this.uuid(index))
      this.form.list.push({value: ''})
    },
    sub (index) {
      this.keyList.splice(index, 1)
      this.form.list.splice(index, 1)
    },
    uuid (index) {
      return `uuid-${index}-${Date.now()}-${Math.random().toFixed(2)}`
    }
  }
}
</script>

<style>
.main-container {
    width: 400px;
}
.main-input {
    width:70%;
}
</style>
