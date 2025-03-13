<script lang="ts">
	import { goto } from '$app/navigation';
	import { API_BASE_URL } from '$lib/api';

	let username = '';
	let password = '';
	let confirmPassword = '';
	let errorMessage = '';

	// 회원가입 처리 함수
	async function handleRegister(event: SubmitEvent) {
		event.preventDefault();

		// 비밀번호 확인 체크
		if (password !== confirmPassword) {
			errorMessage = '비밀번호가 일치하지 않습니다.';
			return;
		}

		const response = await fetch(`${API_BASE_URL}/auth/signup`, {
			method: 'POST',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify({ username, password })
		});
		console.log(response);

		if (response.ok) {
			alert('회원가입 성공! 로그인 페이지로 이동합니다.');
			goto('/login');
		} else {
			const data = await response.json();
			errorMessage = data.error || '회원가입 실패!';
		}
	}
</script>

<form on:submit={handleRegister}>
	<label for="username">아이디</label>
	<input type="text" id="username" bind:value={username} required />

	<label for="password">비밀번호</label>
	<input type="password" id="password" bind:value={password} required />

	<label for="confirmPassword">비밀번호 확인</label>
	<input type="password" id="confirmPassword" bind:value={confirmPassword} required />

	{#if errorMessage}
		<p class="error">{errorMessage}</p>
	{/if}

	<button type="submit">회원가입</button>
</form>


<style>
	form {
		max-width: 400px;
		margin: 0 auto;
		margin-top: 20px;
		padding: 20px;
		border: 1px solid #ccc;
		border-radius: 8px;
		box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
	}

	label {
		display: block;
		margin-bottom: 8px;
		font-weight: bold;
	}

	input {
		width: 100%;
		padding: 8px;
		margin-bottom: 16px;
		border: 1px solid #ccc;
		border-radius: 4px;
	}

	button {
		width: 100%;
		padding: 10px;
		background-color: #007bff;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}

	button:hover {
		background-color: #007bff;
	}

	.error {
		color: red;
		margin-bottom: 10px;
		font-size: 14px;
	}
</style>
