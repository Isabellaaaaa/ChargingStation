<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item>
                    <i class="el-icon-lx-cascades"></i> 设备管理
                </el-breadcrumb-item>
            </el-breadcrumb>    
        </div>  
        <div class="radioGroup">          
            <el-radio-group v-model="currentView" style="margin-bottom: 5px;">
                <el-radio-button label="equipTable">表格模式</el-radio-button>
                <el-radio-button label="equipMap">地图模式</el-radio-button>
            </el-radio-group>
        </div>
        
        <div :is="currentView" keep-alive></div>
    </div>
    
</template>

<script>
import Table from '../EquipmentManagment/EquipmentTable.vue'
import Map from '../EquipmentManagment/EquipmentMap.vue'
  export default {
    components: {
        equipTable: Table,
        equipMap: Map
    },
    data() {
      return {
        currentView: 'equipTable'
      }
    }
  };
</script>

<style scoped>
.radioGroup {
    position: relative;
    /* right: 5px; */
}
</style>