<template>
    <div>
        <h1>Login</h1>
        <button @click="signInWithGoogle">Sign in with Google</button>
    </div>
</template>

<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
    name: 'login',
    layout: 'default',
    setup() {
        
    },
    methods: {
        async signInWithGoogle() {
            const provider = new this.$fireModule.default.auth.GoogleAuthProvider();
            await this.$fire.auth.signInWithPopup(provider).then(res => {
                res.user.getIdToken(true).then(idToken => {
                    localStorage.setItem('access_token', idToken.toString())
                    localStorage.setItem('refresh_token', res.user.refreshToken.toString())
                })
            })
            console.log('login succeeded')
        }
    }
})
</script>
