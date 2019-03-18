<template>
  <div>

    <form @submit.prevent>

      <div class="field">
        <label class="label">Name</label>
        <div class="control">
          <input class="input"
                 :class="{ 'is-danger': isErrorName }"
                 type="text"
                 placeholder="Enter name"
                 v-model="userInfo.name"
                 @input="$v.userInfo.name.$touch()">

          <div v-if="$v.userInfo.name.$error">
            <div class="help is-danger"
                 v-if="!$v.userInfo.name.required">Name is required</div>
            <div class="help is-danger"
                 v-if="!$v.userInfo.name.minLength">Name must have at least {{$v.userInfo.name.$params.minLength.min}} letters.</div>
          </div>

        </div>
      </div>

      <div class="field">
        <label class="label">Email</label>
        <div class="control">
          <input class="input"
                 :class="{ 'is-danger': isErrorEmail }"
                 type="text"
                 placeholder="Enter email"
                 v-model="userInfo.email"
                 @input="$v.userInfo.email.$touch()">

          <div v-if="$v.userInfo.email.$error">
            <div class="help is-danger"
                 v-if="!$v.userInfo.email.required">Email is required</div>
            <div class="help is-danger"
                 v-if="!$v.userInfo.email.email">Email must be a valid email adress.</div>
          </div>

        </div>
      </div>

      <div class="field">
        <label class="label">Phone</label>
        <div class="control">
          <input class="input"
                 :class="{ 'is-danger': isErrorPhone }"
                 type="text"
                 placeholder="Enter phone"
                 v-model="userInfo.phone"
                 @input="$v.userInfo.phone.$touch()">

          <div v-if="$v.userInfo.phone.$error">
            <div class="help is-danger"
                 v-if="!$v.userInfo.phone.required">Phone is required</div>
            <div class="help is-danger"
                 v-if="!$v.userInfo.phone.numeric">Phone must contain only numeric char.</div>
          </div>

        </div>
      </div>

    </form>

    <!-- <pre>{{$v}}</pre> -->

  </div>
</template>

<script>
import { required, minLength, email, numeric } from "vuelidate/lib/validators";

export default {
  name: "CustomForm",
  model: {
    prop: "userInfo"
  },
  props: {
    userInfo: {
      type: Object
    }
  },
  validations: {
    userInfo: {
      name: {
        required,
        minLength: minLength(4)
      },
      email: {
        required,
        email
      },
      phone: {
        required,
        numeric
      }
    }
  },
  computed: {
    isErrorName() {
      return this.$v.userInfo.name.$error;
    },
    isErrorEmail() {
      return this.$v.userInfo.email.$error;
    },
    isErrorPhone() {
      return this.$v.userInfo.phone.$error;
    }
  }
};
</script>

<style scoped>
</style>
