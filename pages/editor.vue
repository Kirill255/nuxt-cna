<template>
  <div>
    <custom-editor v-model="text"></custom-editor>
  </div>
</template>

<script>
import CustomEditor from "~/components/CustomEditor";
export default {
  name: "Editor",
  components: { CustomEditor },
  data: () => ({
    text:""
  })
};
</script>
