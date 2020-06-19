
<template>
    <div id="tab-bar">
  <slot> 
  </slot>
    </div>
</template>

<script>

export default {
  name: 'TabBar',
}
</script>


 <style scoped>
#tab-bar{
  display: flex;
  
  background-color: #cccccc;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  box-shadow: 0 -1px 1px rgba(100, 100, 100, 0.2);/*设置阴影，第一个10PX是x上的，以上的,阴影度，*/
}

</style>




