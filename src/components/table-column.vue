<template>
  <div>
    <tr>
      <th ></th>
    </tr>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props:{
    width:{
      type:String || Number,
    },
    lable:{
      type:String || Number,
      default:'表头'
    }
  },
  mounted() {
    console.log('lable',this.lable);
    console.log('宽度',this.width);
  },
}
</script>