<template>
  <div>
    <custom-form v-model="user"
                 ref="customForm"></custom-form>

    <button type="button"
            class="button is-info m-xs"
            @click="saveUser"
            :disabled="submitStatus === 'PENDING'">Save</button>

    <transition name="notification-fade">
      <div v-if="submitStatus"
           class="notification is-danger">
        <p class="is-size-5"
           v-if="submitStatus === 'OK'">Thanks for your submission!</p>
        <p class="is-size-5"
           v-if="submitStatus === 'ERROR'">Please fill the form correctly.</p>
        <p class="is-size-5"
           v-if="submitStatus === 'PENDING'">Sending...</p>
      </div>
    </transition>

  </div>
</template>

<script>
import CustomForm from "~/components/CustomForm";
export default {
  name: "user",
  components: { CustomForm },
  data: () => ({
    user: {
      name: "",
      email: "",
      phone: ""
    },
    submitStatus: null
  }),
  methods: {
    saveUser() {
      console.log("Try submit!");
      this.$refs.customForm.$v.$touch();

      if (this.$refs.customForm.$v.$invalid) {
        this.submitStatus = "ERROR";

        setTimeout(() => {
          this.submitStatus = null;
        }, 2000);

        console.log("Some user field is empty!");
      } else {
        // do your submit logic here
        this.submitStatus = "PENDING";

        setTimeout(() => {
          this.submitStatus = "OK";

          this.user.name = "";
          this.user.email = "";
          this.user.phone = "";
          this.$refs.customForm.$v.$reset();

          setTimeout(() => {
            this.submitStatus = null;
          }, 2000);

          console.log("user :", this.user);
        }, 1000);
      }
    }
  }
};
</script>

<style scoped>
.notification-fade-enter-active,
.notification-fade-leave-active {
  transition: opacity 0.5s;
}
.notification-fade-enter,
.notification-fade-leave-to {
  opacity: 0;
}
</style>

/*
Почему-то стили скачут при обновлении страницы, если обновиться на главной и потом перейти по ссылкам то всё нормально, косяк ssr наверно, как исправить пока недумал, может подключить bulma.css только если process.browser или ещё что, возможно нужно ещё убрать лишние div'ы обёртки
*/
