<template>
	<div class="signin-container">
		<img src="../assets/icon.png" alt="Codeway Logo" class="logo" />
		<div class="signin-box">
			<h2>Please sign in</h2>
			<form @submit.prevent="signIn">
				<div class="input-container">
					<input type="email" placeholder="E-mail address" v-model="email" required />
					<input type="password" placeholder="Password" v-model="password" required />
				</div>
				<div class="button-container">
					<button type="submit">Sign in</button>
				</div>
			</form>
			<div class="copyright">
				<p>Codeway © 2021</p>
			</div>
		</div>
	</div>
</template>

<script>
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { ref } from 'vue'

export default {
	name: 'SignIn',
	setup() {
		const email = ref('')
		const password = ref('')
		const router = useRouter()
		const store = useStore()

		const signIn = async () => {
			try {
				await store.dispatch('auth/signIn', { email: email.value, password: password.value })
				router.push('/')
			} catch (error) {
				console.error('Authentication error:', error)
				alert('Failed to sign in. Please check your credentials and try again.')
			}
		}

		return {
			email,
			password,
			signIn,
		}
	},
}
</script>

<style scoped>
.signin-container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	font-family: 'Gilmer', sans-serif;
	height: auto;
	width: auto;
	margin-bottom: 200px;
}

.logo {
	max-width: 250px;
	margin-bottom: 30px;
}

h2 {
	color: rgb(50, 50, 91);
	margin-bottom: 10px;
	font-size: 24px;
}

.signin-box {
	display: flex;
	flex-direction: column;
	align-items: center;
	border-radius: 10px;
	padding: 30px;
	text-align: center;
}

.input-container {
	display: flex;
	flex-direction: column;
	width: 100%;
	min-width: 300px;
}

input {
	width: 100%;
	padding: 12px 8px;
	border: 1px solid rgb(47, 54, 83);
	background: none;
	color: rgb(110, 116, 123);
}

input:nth-child(1) {
	border-top-left-radius: 8px;
	border-top-right-radius: 8px;
}

input:nth-child(2) {
	border-bottom-left-radius: 8px;
	border-bottom-right-radius: 8px;
}

input:focus {
	border-color: rgb(216, 92, 204);
	outline: none;
}

input::placeholder {
	font-size: 16px;
}

.button-container {
	widows: 100%;
	margin-top: 10px;
}

button {
	background: linear-gradient(to bottom, rgb(82, 102, 217), rgb(61, 78, 183));
	width: 100%;
	color: #fff;
	padding: 14px 20px;
	border: none;
	border-radius: 8px;
	cursor: pointer;
	font-family: 'Gilmer', sans-serif;
	font-weight: bold;
}

.copyright {
	color: #777;
	margin-top: 6vh;
	font-size: 16px;
}

@media only screen and (max-device-width: 768px) {
	.logo {
		max-width: min(50vw, 250px);
	}
	.signin-container {
		width: 90vw;
	}

	.signin-box {
		width: 100%;
	}

	.input-container {
		min-width: min(300px, 50vw);
	}
}
</style>
