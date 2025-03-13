<script lang="ts">
	import { goto } from '$app/navigation';
	import { API_BASE_URL } from '$lib/api';
	import { construct_svelte_component } from 'svelte/internal';


	let username = '';
	let password = '';

	// 로그인 처리 함수
	const login = async () => {
    try {
      // 로그인 요청
      const response = await fetch(`${API_BASE_URL}/auth/signin`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ username, password }),
      });

      if (!response.ok) {
        throw new Error('로그인에 실패했습니다.');
      }                 

      const data = await response.json();

      // JWT 토큰을 localStorage에 저장
    //   localStorage.setItem('jwt_token', data.accessToken);

	  if (typeof window !== 'undefined') {
		localStorage.setItem('jwt_token', data.accessToken);
	  }

      console.log('로그인 성공!', data);
	  goto('/');
    } catch (error) {
    //   errorMessage = error.message;
    }
  };
</script>

<form on:submit|preventDefault={login}>
	<label for="username">아이디</label>
	<input type="text" id="username" bind:value={username} required />

	<label for="password">비밀번호</label>
	<input type="password" id="password" bind:value={password} required />

	<button type="submit">로그인</button>
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
		background-color: #0056b3;
	}
</style>
