
<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="test" style="width:100%; height:620px;">
        <div>child:这是父组件给我传的数据——{{jsonData.name}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "test",
  props: ["jsonData"],
  data() {
    return {};
  }

  //   props: {
  //     transmitData: {
  //       type: String,
  //       default: "hello world"
  //     }
  //   }
};
</script>