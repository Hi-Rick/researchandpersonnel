<template>
    <div class="app-container">
      <el-row :gutter="20">
        <div style="display: flex;align-items: center;margin: 15px 0;">
          <div style="font-size: 14px;margin: 0 15px;font-weight: bolder">请选择学院:</div>
          <div>
            <el-select v-model="value" placeholder="请选择学院">
              <el-option label="文学院" value="1"></el-option>
              <el-option label="理学院" value="2"></el-option>
              <el-option label="教育学院" value="3"></el-option>
              <el-option label="医学院" value="4"></el-option>
              <el-option label="商学院" value="5"></el-option>
              <el-option label="管理学院" value="6"></el-option>
              <el-option label="机械工程学院" value="7"></el-option>
              <el-option label="电子信息学院" value="8"></el-option>
              <el-option label="电气工程学院" value="9"></el-option>
            </el-select>
          </div>
          <div style="font-size: 14px;margin-right: 15px;font-weight: bolder;margin-left: 15px">请选择部门:</div>
          <div>
            <el-select v-model="value1" placeholder="请选择部门">
              <el-option label="校党委" value="1"></el-option>
              <el-option label="教务处" value="2"></el-option>
              <el-option label="科研处" value="3"></el-option>
              <el-option label="电教设备处" value="4"></el-option>
              <el-option label="审计处" value="5"></el-option>
              <el-option label="档案中心" value="6"></el-option>
            </el-select>
          </div>
          <div style="font-size: 14px;margin: 0 15px;font-weight: bolder">请输入教师姓名:</div>
          <div>
            <el-input v-model="input" placeholder="请输入姓名"/>
          </div>
          <div>
            <el-button type="primary" style="margin-left:15px" @click="query">查询</el-button>
          </div>
        </div>
      </el-row>
      <el-divider/>
      <el-row>
          <el-table
            :data="tableData"
            border
            style="width: 100%">
            <el-table-column
              prop="number"
              align="center"
              label="编号"
              width="50">
            </el-table-column>
            <el-table-column
              prop="name"
              label="教师姓名"
              align="center"
              width="160">
            </el-table-column>
            <el-table-column
              prop="college"
              label="学院"
              align="center"
              width="160">
            </el-table-column>
            <el-table-column
              prop="department"
              label="部门"
              align="center"
              width="160">
            </el-table-column>
            <el-table-column
              prop="title"
              align="center"
              label="职称"
              width="140">
            </el-table-column>
            <el-table-column prop="quanxian" align="center" label="权限展示">
<!--                        <template slot-scope="scope">-->
<!--                          <el-select v-model="scope.row.userrole" placeholder="权限" @change="eidtAuthority(scope.row.userid, scope.row.userrole)">-->
<!--                            <el-option label="教师" value="教师"/>-->
<!--                            <el-option label="系部主管" value="系部主管"/>-->
<!--                            <el-option label="科研主管" value="科研主管"/>-->
<!--                          </el-select>-->
<!--                        </template>-->
<!--              <template slot-scope="scope">-->
<!--                <div v-for="(item,i) in scope.row.userrole" :key="i">-->
<!--                  <span>{{ item }}</span>-->
<!--                </div>-->
<!--              </template>-->
            </el-table-column>
            <el-table-column align="center" label="权限设置"  width="250px">
<!--                        <template slot-scope="scope">-->
<!--                          <el-select v-model="scope.row.userrole" placeholder="权限" @change="eidtAuthority(scope.row.userid, scope.row.userrole)">-->
<!--                            <el-option label="教师" value="教师"/>-->
<!--                            <el-option label="系部主管" value="系部主管"/>-->
<!--                            <el-option label="科研主管" value="科研主管"/>-->
<!--                          </el-select>-->
<!--                        </template>-->
              <template slot-scope="scope">
                <el-select v-model="scope.row.edit" multiple placeholder="请选择权限" style="width: 120px">
                  <el-option label="教师" value="教师"/>
                  <el-option label="系部主管" value="系部主管"/>
                  <el-option label="科研主管" value="科研主管"/>
                </el-select>
                <el-button type="primary" style="margin-top: 10px" @click="change">确认修改</el-button>
              </template>
            </el-table-column>
          </el-table>
        <div class="fenye">
          <el-pagination
            :current-page="currentPage"
            :page-sizes="[10, 20, 30]"
            :page-size="10"
            style="margin-top:20px;"
            :total= "5"
            layout="total, sizes, prev, pager, next, jumper"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
          />
        </div>
      </el-row>
    </div>
</template>

<script>
    export default {
        name: "index",
      filters: {
        statusFilter(status) {
          const statusMap = {
            published: 'success',
            draft: 'info',
            deleted: 'danger'
          }
          return statusMap[status]
        }
      },
      data() {
        return {
          currentPage:'1',
          tableData: [{
            number:'1',
            name: '王老师',
            sex: '女' ,
            college:'文学院',
            department: '科研处',
            title: '讲师',
            quanxian:'教师',
          }, {
            number:'2',
            name: '李老师',
            sex: '男' ,
            college:'理学院',
            department: '教务处',
            title: '教授',
            quanxian:'教师 科研主管',
          }, {
            number:'3',
            name: '刘老师',
            sex: '女' ,
            college:'文学院',
            department: '审计处',
            title: '讲师',
            quanxian:'教师 系部主管',
          }, {
            number:'4',
            name: '赵老师',
            sex: '女' ,
            college:'管理学院',
            department: '电教设备处',
            title: '讲师',
            quanxian:'教师 系部主管 科研主管',
          },
            {
              number:'5',
              name: '张老师',
              sex: '女' ,
              college:'机械工程学院',
              department: '科研处',
              title: '讲师',
              quanxian:'教师 系部主管',
            }],
          pagesize: 10,
          currentPage: 1,
          value1: '',
          input: '',
          value: '',
          dialogPvVisible: false,
          thisId: ''
        }
      },
      created() {
      },
      methods: {
        cancelEdit(row) {
          row.title = row.originalTitle
          row.edit = false
          this.$message({
            message: 'The title has been restored to the original value',
            type: 'warning'
          })
        },
        query(){
          if(this.value!==''){
            this.$message({
              message: '查询成功',
              type: 'success'
            });
          } else {
            this.$message({
              message: '请添加选项查询',
              type: 'warning'
            });
          }
        },
        change(){
            this.$message({
              message: '修改成功',
              type: 'success'
            });
        },
        handleSizeChange(val) {
          console.log(`每页 ${val} 条`)
          this.pagesize = val
        },
        handleCurrentChange(val) {
          console.log(`当前页: ${val}`)
          this.currentPage = val
        }
      }
    }
</script>

<style scoped>
  .edit-input {
    padding-right: 100px;
  }
  .cancel-btn {
    position: absolute;
    right: 15px;
    top: 10px;
  }
  .fenye {
    text-align: center;
  }
</style>
