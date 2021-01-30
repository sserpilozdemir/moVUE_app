<template>
  <div>
    <app-navbar></app-navbar>
    <router-view></router-view>
    
  </div>
</template>
<script>
import appNavbar from "@/components/appNavbar";
import appSearch from "@/components/appSearch";
export default {
  components: {
    appNavbar,
    appSearch
  },
};
</script>