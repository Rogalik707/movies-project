<script>
export default {
  setup() {
    const email = ref('');
    const isEmptyInput = ref(true);
    const isValidEmail = ref(false);

    const isInputValid = () => {
      email.value === '' ? isEmptyInput.value = true : isEmptyInput.value = false;
    }

    const isEmailValid = () => {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(String(email.value).toLowerCase());
    }
    watch(email, () => {
      isInputValid();
      isValidEmail.value = isEmailValid();
    })

    return {
      email,
      isEmptyInput,
      isValidEmail,
    };
  }
};
</script>

<template>
  <main>
    <div class="bg">
      <h1>Movie Matching</h1>
      <div class="bg-circle"/>
      <div class="bg-circle-blue"/>
    </div>
    <div class="input-container">
      <label class="input-label">
        <span class="input-placeholder">enter your friend's email address</span>
        <input v-model="email" class="input" type="email"/>
      </label>
      <NuxtLink to="choosing-genre" :class="{'input-accept': isValidEmail && !isEmptyInput, 'disable': !isValidEmail || isEmptyInput}">
        <h1>➜</h1>
      </NuxtLink>
    </div>
  </main>
</template>

<style lang="scss">
.bg {
  & > h1 {
    padding-top: 40px;
  }
}

.input-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

.input-accept {
  position: relative;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: rgb(0, 77, 239);
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  box-shadow: 0 0 900px rgb(0, 77, 239);


  & > h1 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 30px;
    color: white;
  }

  &:hover {
    background-color: #91a5da;

    & > h1 {
      color: rgb(7, 52, 148);
    }
  }
}

.disable {
  position: relative;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: rgb(82, 82, 82);
  cursor: default;
  transition: all 0.3s ease-in-out;
  box-shadow: 0 0 900px rgb(0, 77, 239);

  & > h1 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 30px;
    color: #868686;
  }
}

.input-label {
  width: 300px;
  height: 50px;
  border-radius: 50px;

}

.input {
  width: 100%;
  height: 100%;
  border-radius: 50px;
  border: none;
  outline: none;
  padding: 0 20px;
  font-size: 20px;
  font-weight: bold;
  color: #000000;
  font-family: "HP Simplified", serif;

  &-placeholder {
    position: absolute;
    top: 2px;
    left: 20px;
    font-size: 12px;
    font-weight: bold;
    color: rgba(0, 0, 0, 0.36);
    font-family: "HP Simplified", serif;
  }
}
</style>
