<template>
<div class="progress">
      <div class="progress-bar bg-info" role="progressbar" :style="{width : progresscount + '%'}" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">
        {{currentItem}}/10
      </div>
    </div>
</template>

<script>
import {eventBus} from "../main";
export default {
  data(){
    return {
      currentItem : 0,
      progresscount : 0
    }
  },
  created(){
    eventBus.$on("progressBar", (barcurrent) => {
      this.currentItem = barcurrent;
      this.progresscount = barcurrent * 10
    })
  }
}
</script>