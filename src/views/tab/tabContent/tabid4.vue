<template>
    <section class="adminContentContainer">
        <section class="adminContentInner">
            <el-form :inline="true" :model="formInline" class="demo-form-inline">
                <el-form-item label="会员ID">
                    <el-input v-model="formInline.user" placeholder="会员ID"></el-input>
                </el-form-item>
                <el-form-item label="姓名">
                    <el-input v-model="formInline.user" placeholder="请输入姓名"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">查询</el-button>
                </el-form-item>
            </el-form>
            <div class="block">
                <el-table
                    :data="tableData"
                    border
                    highlight-current-row
                    @current-change="handleCurrentChange"
                    style="width: 100%">
                    <el-table-column
                        prop="changeId"
                        label="反馈ID">
                    </el-table-column>
                    <el-table-column
                        prop="id"
                        label="会员ID">
                    </el-table-column>
                    <el-table-column
                        prop="name"
                        label="姓名">
                    </el-table-column>
                    <el-table-column
                        prop="feedBackcontent"
                        label="反馈内容">
                    </el-table-column>
                    <el-table-column
                        prop="auditState"
                        label="状态">
                    </el-table-column>
                    <el-table-column
                        prop="registerTime"
                        label="反馈时间">
                    </el-table-column>
                    <el-table-column
                        prop="auditer"
                        label="变更人">
                    </el-table-column>
                </el-table>
                <div class="block adminPage">
                    <!--<span class="demonstration">完整功能</span>-->
                    <el-pagination
                        background
                        @size-change="handleSizeChange"
                        @current-change="handleCurrentChange"
                        :current-page="currentPage4"
                        :page-sizes="[100, 200, 300, 400]"
                        :page-size="100"
                        layout="total, sizes, prev, pager, next, jumper"
                        :total="400">
                    </el-pagination>
                </div>
                <div class="block adminAuditControl">
                    <el-form :inline="true" class="demo-form-inline">
                        <el-form-item>
                            <el-button @click.native="detailInfo">详情</el-button>
                        </el-form-item>
                    </el-form>
                </div>
            </div>
        </section>
        <el-dialog
            :title="selectedData.name+'的反馈信息'"
            :visible.sync="centerDialogVisible"
            width="30%"
            center>
            <div class="block">
                <p>
                    {{selectedData.feedBackcontent}}
                </p>
            </div>
            <div class="block">
                <el-form :inline="true" class="demo-form-inline">
                <el-form-item label="输入反馈回复" :inline="true" class="rejectAuditInline">
                    <textarea class="feedBackArea" style="resize: none;" name="" id="" cols="30" rows="10"></textarea>
                </el-form-item>
                </el-form>
            </div>
            <span slot="footer" class="dialog-footer">
            <el-button @click="centerDialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="feedBackContent()">回复</el-button>
            </span>
        </el-dialog>
    </section>
</template>
<script>
    import userData from '../../../virtualData/feedback';
    export default {
        data(){
            return {
                formInline: {
                    user: '',
                    region:''
                },
                rejectAuditReason:"",
                selectedData:{},
                centerDialogVisible:false,
                selectedOne:false,
                msg:"",
                currentPage4:4,
                tableData:userData.data.dataList
            }
        },
        methods:{
            feedBackContent(){
              let t = this;
              t.centerDialogVisible = false;
                t.$message({
                    message: t.selectedData.name+'反馈信息已回复',
                    type: 'success'
                });
            },
            handleSelectionChange(val) {
                this.multipleSelection = val;
            },
            detailInfo(){
              let t = this;
              if(!t.selectedOne){
                  t.$message.error('请选择您要变更的用户!');
              }else{
                  t.centerDialogVisible = true;
              }
            },
            onSubmit() {
                console.log('submit!');
            },
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
                let t = this;
                t.selectedOne = true;
                t.selectedData = val;
            }
        }
    }
</script>
<style lang="scss" scoped>
    @import "../../../styleComponent/ContentInner";
    .adminContentInner{
        @include ContentInner();
        .adminUserControl{
            padding: 0 0 10px 0;
        }
        .adminPage{
            padding: 20px 0;
        }
        .adminAuditControl{
            padding: 20px 0;
        }
    }
    .block{
        padding: 20px 0;
    }
    .rejectAuditInline,.feedBackArea{
        width: 100%;
        height: 100%;
        margin: 0 auto;
        textarea{
            width: 383.7px;
            height: 265.8px;
        }
    }
</style>
