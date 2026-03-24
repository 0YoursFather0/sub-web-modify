<template>
  <div class="subconverter-page">
    <el-row class="subconverter-layout" style="margin-top: 10px">
      <el-col>
        <el-card class="subconverter-card">

          <el-container class="subconverter-container">
            <el-form class="subconverter-form" :model="form" label-width="92px" label-position="left" style="width: 100%">

              <el-form-item label="订阅链接:">
                <el-input v-model="form.sourceSubUrl" type="textarea" rows="3"/>
              </el-form-item>

              <el-form-item label="生成类型:">
                <el-select v-model="form.clientType" style="width: 100%">
                  <el-option v-for="(v, k) in options.clientTypes" :key="k" :label="k" :value="v"/>
                </el-select>
              </el-form-item>

              <el-form-item label="后端地址:">
                <el-select v-model="form.customBackend" style="width: 100%"/>
              </el-form-item>

              <el-form-item label="远程配置:">
                <el-select v-model="form.remoteConfig" style="width: 100%"/>
              </el-form-item>

              <!-- 输出 -->
              <el-form-item label="定制订阅:">
                <el-input disabled v-model="customSubUrl"/>
              </el-form-item>

              <el-form-item label="订阅短链:">
                <el-input v-model="customShortSubUrl"/>
              </el-form-item>

              <!-- ✅ 关键修改在这里 -->
              <el-form-item label-width="0px" style="margin-top: 40px; text-align: center">

                <!-- 第一排 -->
                <div style="display:flex;justify-content:center;gap:12px;flex-wrap:wrap">

                  <el-button
                    type="danger"
                    style="width:140px"
                    @click="makeUrl"
                    :disabled="form.sourceSubUrl.length === 0"
                  >
                    生成订阅链接
                  </el-button>

                  <el-button
                    type="danger"
                    style="width:140px"
                    @click="makeShortUrl"
                    :disabled="customSubUrl.length === 0"
                  >
                    生成短链接
                  </el-button>

                </div>

                <!-- 第二排（新增） -->
                <div style="margin-top:16px;display:flex;justify-content:center;gap:12px;flex-wrap:wrap">

                  <el-button
                    type="primary"
                    @click="dialogUploadConfigVisible = true"
                  >
                    自定义配置
                  </el-button>

                  <el-button
                    type="primary"
                    @click="dialogLoadConfigVisible = true"
                  >
                    从URL解析
                  </el-button>

                </div>

              </el-form-item>

            </el-form>
          </el-container>

        </el-card>
      </el-col>
    </el-row>

    <!-- ✅ URL解析弹窗（你原本就有） -->
    <el-dialog :visible.sync="dialogLoadConfigVisible" width="500px">
      <div slot="title">从URL解析</div>

      <el-input v-model="loadConfig" type="textarea" rows="5"/>

      <span slot="footer">
        <el-button @click="dialogLoadConfigVisible = false">取消</el-button>
        <el-button type="primary" @click="confirmLoadConfig">解析</el-button>
      </span>
    </el-dialog>

  </div>
</template>
