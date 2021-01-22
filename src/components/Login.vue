<template>
    <div>
        <label>
            user:<input type="text" v-model="loginForm.username">
        </label>
        <br><br>
        <label>
            password:<input type="password" v-model="loginForm.password">
        </label>
        <br><br>
        <button type="button" @click="login">login</button>
    </div>
</template>

<script>
export default {
    name: 'Login.vue',
    data () {
        return {
            loginForm: {
                username: '',
                password: ''
            },
            responseResult: []
        }
    },
    methods: {
        login () {
            this.$axios
                .post('/login', {
                    username: this.loginForm.username,
                    password: this.loginForm.password
                })
                .then(successResponse => {
                    if (successResponse.data.code === 200) {
                        this.$router.replace({path: '/index'})
                    } else if (successResponse.data.code === 400) {
                        alert('failed.')
                    }
                })
                .catch(failResponse => {
                })
        }
    }
}
</script>

<style scoped>

</style>
