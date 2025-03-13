<script lang="ts">
</script>

<style>
	nav {
		background-color: #007bff;
		color: white;
		padding: 16px;
		display: flex;
		align-items: left;
	}

	a {
		color: white;
		font-weight: bold;
        padding: 20px;
	}

	a:hover {
		color: #d4d4d4;
	}
</style>

<nav>
    <a href="/">Home</a>
    <a href="/register">Register</a>
    <a href="/login">Login</a>
	<a href="/user">Mypage</a>
</nav>

<main>
	<slot/>
</main>
