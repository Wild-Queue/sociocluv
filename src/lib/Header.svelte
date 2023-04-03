<script lang="ts">
    import Card from "$lib/Card.svelte"
</script>

<Card>
    <div slot="card-body">
        <nav>
            <a href="/">Register</a>
            <a href="/elonmusk">Profile</a>
            <a href="/home">Feed</a>
            <a href="/elonmusk/status/4">Single Tweet</a>
        </nav>
    </div>
</Card>

<style>
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem;
        background: white;
    }
    nav a {
        color: #333;
        text-decoration: none;
        margin: 0 0.5rem;
    }
    nav a:hover {
        color: #555;
    }
</style>