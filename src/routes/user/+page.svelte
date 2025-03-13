<script lang="ts">
    import { API_BASE_URL } from '$lib/api';
	import { onMount } from 'svelte';

    let token : any;
    let errorMessage = '';
    let user: any;
    let username = '';

    // const token = localStorage.getItem('jwt_token');

    onMount(async () => {
        if (typeof window !== 'undefined') {
            token = localStorage.getItem('jwt_token');
        }
        if (!token) {
            errorMessage = "로그인이 필요합니다.";
            return;
        }
    
        const response = await fetch(`${API_BASE_URL}/auth/me`, {
            method: 'GET',
            headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${token}`,
            } 
        });

        if (response.ok) {
            user = await response.json();
            console.log(user);
        }
        username = user.user.username;
    })


</script>


{#if username}
	<h1>안녕하세요, {username}님!</h1>
{/if}