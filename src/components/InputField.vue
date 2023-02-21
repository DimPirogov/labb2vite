<script>
export default {
  data() {
    return {
      textArea: "",
      eMail: "",
      state: false,
      message: "Tell us what you think",
    };
  },
  methods: {
    onSubmit(event) {
      if (event) {
        this.message = "Vi received your input!";
        this.state = true;
        event.preventDefault();
      }
    },
  },
};
</script>
<template>
  <div class="containter">
    <form @submit="onSubmit">
      <div class="form-group">
        <label for="exampleFormControlTextarea1">{{ message }}</label>
        <textarea
          :disabled="state"
          v-model="textArea"
          class="form-control"
          id="exampleFormControlTextarea1"
          rows="3"
        ></textarea>
      </div>
      <div v-if="!state">
        <div class="form-group">
          <label for="exampleInputEmail1">Email address</label>
          <input
            v-model="eMail"
            type="email"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
          />
          <small id="emailHelp" class="form-text text-muted"
            >We'll never share your email with anyone else. Please fill both
            input fields.</small
          >
        </div>
        <input
          type="submit"
          class="btn btn-primary"
          :disabled="!eMail || !textArea"
          value="Send it"
        />
      </div>
    </form>
  </div>
</template>
