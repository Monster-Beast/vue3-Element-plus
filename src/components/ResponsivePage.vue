<template>
  <el-container>
    <el-main>
      <el-row :gutter="20">
        <el-col :span="24">
          <el-form :inline="true" :model="form" class="demo-form-inline">
            <el-row :gutter="20">
              <el-col :span="6">
                <el-form-item label="开始时间">
                  <el-date-picker
                    v-model="form.startDate"
                    type="daterange"
                    start-placeholder="开始时间"
                    end-placeholder="结束时间"
                    style="width: 100%;"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="6">
                <el-form-item label="结束时间">
                  <el-date-picker
                    v-model="form.endDate"
                    type="daterange"
                    start-placeholder="开始时间"
                    end-placeholder="结束时间"
                    style="width: 100%;"
                  />
                </el-form-item>
              </el-col>
              <el-col :span="6">
                <el-form-item label="工作流名称">
                  <el-input v-model="form.workflowName" placeholder="请输入工作流名称" />
                </el-form-item>
              </el-col>
              <el-col :span="6">
                <el-form-item label="工程名称">
                  <el-input v-model="form.projectName" placeholder="请输入工程名称" />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20">
              <el-col :span="6">
                <el-form-item label="工作流 ID">
                  <el-input v-model="form.workflowId" placeholder="请输入工作流 ID" />
                </el-form-item>
              </el-col>
              <el-col :span="6">
                <el-form-item label="实例名称">
                  <el-input v-model="form.instanceName" placeholder="请输入实例名称" />
                </el-form-item>
              </el-col>
              <el-col :span="6">
                <el-form-item label="启动用户">
                  <el-input v-model="form.user" placeholder="请输入启动用户" />
                </el-form-item>
              </el-col>
              <el-col :span="6">
                <el-form-item label="所属服务器">
                  <el-input v-model="form.server" placeholder="请输入所属服务器" />
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20">
              <el-col :span="6">
                <el-form-item>
                  <el-button type="primary" @click="onSearch">查询</el-button>
                  <el-button @click="onReset">重置</el-button>
                </el-form-item>
              </el-col>
            </el-row>
            <el-row :gutter="20">
              <el-col :span="6">
                <el-form-item>
                  <el-button @click="onExportAll">导出</el-button>
                </el-form-item>
              </el-col>
            </el-row>
          </el-form>
        </el-col>
      </el-row>

      <el-row :gutter="20" style="margin-top: 20px;">
        <el-col :span="24">
          <el-table :data="tableData" style="width: 100%">
            <el-table-column type="index" label="序号" width="50"></el-table-column>
            <el-table-column prop="workflowName" label="工作流名称"></el-table-column>
            <el-table-column prop="projectName" label="工程名称"></el-table-column>
            <el-table-column prop="workflowId" label="工作流 ID"></el-table-column>
            <el-table-column prop="instanceName" label="实例名称"></el-table-column>
            <el-table-column prop="status" label="状态">
              <template #default="scope">
                <el-tag :type="getStatusTagType(scope.row.status)">{{ scope.row.status }}</el-tag>
              </template>
            </el-table-column>
            <el-table-column prop="user" label="启动用户"></el-table-column>
            <el-table-column prop="startTime" label="开始时间"></el-table-column>
            <el-table-column prop="endTime" label="结束时间"></el-table-column>
            <el-table-column prop="server" label="所属服务器"></el-table-column>
            <el-table-column label="操作">
              <template #default="scope">
                <el-button @click="onExport(scope.row)" type="text">导出</el-button>
              </template>
            </el-table-column>
          </el-table>
          <el-pagination
            background
            layout="sizes, prev, pager, next, jumper, ->, total"
            :total="100"
            :page-sizes="[10, 20, 30, 40]"
            :page-size="10"
            style="margin-top: 20px;"
          ></el-pagination>
        </el-col>
      </el-row>
    </el-main>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      form: {
        date: '',
        workflowId: '',
        instanceName: '',
        user: '',
        server: ''
      },
      tableData: [
        // 模拟数据
        {
          workflowName: '工作流1',
          projectName: '工程1',
          workflowId: '001',
          instanceName: '实例1',
          status: '运行中',
          user: '用户1',
          startTime: '2023-01-01',
          endTime: '2023-01-02',
          server: '服务器1'
        }
      ]
    }
  },
  methods: {
    onSearch() {
      // 查询逻辑
      console.log('查询', this.form);
    },
    onReset() {
      this.form = {
        date: '',
        workflowId: '',
        instanceName: '',
        user: '',
        server: ''
      };
    },
    onExport(row) {
      // 导出逻辑
      console.log('导出', row);
    },
    getStatusTagType(status) {
      switch (status) {
        case '运行中':
          return 'success';
        case '已完成':
          return 'info';
        default:
          return 'warning';
      }
    }
  }
}
</script>

<style>
.el-menu-demo {
  background-color: #545c64;
  color: #fff;
}
.demo-form-inline .el-form-item {
  margin-right: 20px;
}
</style>
