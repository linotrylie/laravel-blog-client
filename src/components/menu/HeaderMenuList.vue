<template>
    <div style="display: inline">
        <el-menu
                 :default-active="activeIndex"
                 mode="horizontal"
                 active-text-color="#ffd04b"
                 class="el-menu-demo"
        >
            <template v-for="menu in data">
                <el-submenu v-if="menu.all_home_menu.length > 0" :index="menu.router" :key="menu.id">
                    <template slot="title">{{menu.menu_name}}</template>
                        <app-menu-list :data="menu.all_home_menu"></app-menu-list>
                </el-submenu>
                    <el-menu-item v-else :index="menu.router" :key="menu.id">
                        <label>
                            <router-link :to="menu.router">
                                {{menu.menu_name}}
                            </router-link>
                        </label>
                    </el-menu-item>
            </template>
        </el-menu>
    </div>
</template>

<script>
import HeaderMenuList from '@/components/menu/HeaderMenuList'
export default {
  name: 'app-menu-list',
  data () {
    return {
      activeIndex: '/',
      menuData: {}
    }
  },
  components: {HeaderMenuList},
  props: ['data']
}

</script>

<style scoped>

</style>
