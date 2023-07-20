<template>
    <form @submit.prevent="formSubmit" class="card">
        <p class="title">Enter your password</p>
        <article class="information">
            <img src="@/assets/images/user-photo.png" alt="user-photo">
            <div class="information-list">
                <p class="information-item">Business Account</p>
                <p class="information-item -name">Sarah Bills</p>
            </div>
        </article>
        <article class="entry">
            <p class="title -password">Password</p>
            <div class="entry-area">
                <img class="entry-area__icon" src="@/assets/icons/lock-icon.svg" alt="lock-icon">
                <input class="input -password" :type="inputType" v-model="inputValue" @input="validatePassword" required>
                <img :src="iconUrl" alt="toggle-icon" @click="togglePassword">
                <div v-if="inputValue && !passwordFlag" class="tooltip">Password must contain at least 1 uppercase letter, lowercase letter, number, special character. More than 8 characters.</div>
            </div>
        </article>
        <article class="submit">
            <div class="submit-items">
                <label class="switch">
                    <input class="switch-input" type="checkbox" v-model="checkboxFlag"/>
                    <span class="switch-slider -round"></span>
                </label>
                <p class="desc">Stay signed in</p>
            </div>
            <button id="submit-button" class="btn" :disabled="!passwordFlag">Continue</button>
        </article>
    </form>
</template>
<script>

export default {
    name: 'PasswordView',
    data() {
        return {
            inputValue:"",
            inputType: "password",
            iconUrl: require("@/assets/icons/eye-not-look-icon.svg"),
            passwordFlag: false,
            checkboxFlag: false,
        }
    },
    methods: {
        togglePassword() {
            this.inputType = this.inputType === "password" ? "text" : "password";
            this.iconUrl = this.inputType === "password"
                ? require("@/assets/icons/eye-not-look-icon.svg")
                : require("@/assets/icons/eye-look-icon.svg");
        },
        validatePassword() {
            const passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&.])[A-Za-z\d@$!%*?&.]{8,}$/;
            this.passwordFlag = passwordPattern.test(this.inputValue);
        },
        formSubmit () {
            console.log(
                {
                    value: this.inputValue,
                    isStatus: this.checkboxFlag
                }
            )
        }
    }
}
</script>

<style lang="scss" scoped>
.card {
    display: flex;
    padding: $sp-xxl;
    flex-direction: column;
    align-items: flex-start;
    gap: $sp-lg;
    border-radius: $r-md;
    background: $white;
    box-shadow: $min-shadow;

    &::before {
        content: "";
        z-index: -1;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        opacity: 0.04;
        background-color: $catalina-blue;
    }
}
</style>