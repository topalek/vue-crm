<template>
  <form @submit.prevent="submitHandler" class="card auth-card">
    <div class="card-content">
      <span class="card-title">Домашняя бухгалтерия</span>
      <div class="input-field">
        <input
            :class="{
            invalid:
              ($v.email.$dirty && !$v.email.required) ||
              ($v.email.$dirty && !$v.email.email)
          }"
            id="email"
            type="text"
            v-model.trim="email"
        />
        <label for="email">Email</label>
        <small
            class="helper-text invalid"
            v-if="$v.email.$dirty && !$v.email.required"
        >Заполните Email</small
        >
        <small
            class="helper-text invalid"
            v-else-if="$v.email.$dirty && !$v.email.email"
        >Введите корректный Email</small
        >
      </div>
      <div class="input-field">
        <input
            :class="{
            invalid: ($v.password.$dirty && !$v.password.required) || ($v.password.$dirty && !$v.password.minLength)
          }"
            id="password"
            type="password"
            v-model.trim="password"
        />
        <label for="password">Пароль</label>
        <small
            class="helper-text invalid"
            v-if="$v.password.$dirty && !$v.password.required"
        >Заполните Пароль</small
        >
        <small
            class="helper-text invalid"
            v-else-if="$v.password.$dirty && !$v.password.minLength"
        >Пароль должен быть более {{ $v.password.$params.minLength.min }} символов</small
        >
      </div>
      <div class="input-field">
        <input
            :class="{
            invalid: $v.name.$dirty && !$v.name.required
          }"
            id="name"
            type="text"
            v-model.trim="name"
        />
        <label for="name">Имя</label>
        <small
            class="helper-text invalid"
            v-if="$v.name.$dirty && !$v.name.required"
        >Заполните Имя</small
        >
        <small
            class="helper-text invalid"
            v-else-if="$v.name.$dirty && !$v.name.minLength"
        >Имя должно быть более {{ $v.name.$params.minLength.min }} символов</small
        >
      </div>
      <p>
        <label>
          <input type="checkbox" v-model="agree"/>
          <span>С правилами согласен</span>
        </label>
      </p>
    </div>
    <div class="card-action">
      <div>
        <button class="btn waves-effect waves-light auth-submit" type="submit">
          Зарегистрироваться
          <i class="material-icons right">send</i>
        </button>
      </div>

      <p class="center">
        Уже есть аккаунт?
        <router-link to="/login">Войти!</router-link>
      </p>
    </div>
  </form>
</template>

<script>
import {email, minLength, required} from "vuelidate/lib/validators";

export default {
  name: "register",
  data: () => ({
    email: "",
    password: "",
    name: "",
    agree: false
  }),
  validations: {
    email: {email, required},
    name: {required, minLength: minLength(2)},
    password: {required, minLength: minLength(6)},
    agree: {checked: v=> v}
  },
  methods: {
    submitHandler() {
      console.log(this.$v.agree, this.$v.name,);
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      const formData = {
        email: this.email,
        password: this.password,
        name: this.name
      }
      console.log(formData);
      this.$router.push("/");
    }
  }
};
</script>
