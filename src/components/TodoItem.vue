<template>
  <div>
    <el-col :span="12">
      <el-card class="box-card" shadow="hover" style="margin: 5px 0;">
        <el-row :gutter="12">
          <el-col :span="21">{{ item.title || item }}</el-col>
          <el-col :span="3">
            <el-button @click="RemoveTodo" type="success" icon="el-icon-check" circle></el-button>
            
          </el-col>
        </el-row>
      </el-card>
    </el-col>
  </div>
</template>
<script>
  export default {
    name: 'TodoItem',
    props: { // requeridoo
      todo: {
        type: String,
        required: true
      },
      issue: {
        type: String,
        required: false
      },
      index: {
        type: Number,
        required: true
      },
    },
    methods: {
      RemoveTodo() {
        if (this.type === 'todo') {
        this.$emit('remove-todo', this.index);
      } else if (this.type === 'issue') {
        this.$emit('close-issue', this.index);
      }
    }
  }
  }
  </script>