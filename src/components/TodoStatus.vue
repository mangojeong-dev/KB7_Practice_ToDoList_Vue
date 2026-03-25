<template>
  <div>
    <span>전체 todo 개수: {{ cnt[0] }}</span>
    <span>완료 todo 개수: {{ cnt[1] }}</span>
    <span>미완료 todo 개수: {{ cnt[2] }}</span>
  </div>
</template>

<script>
export default {
  name: 'TodoStatus',
  props: ['cnt'],
};
</script>
