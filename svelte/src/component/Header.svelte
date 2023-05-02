<script>
    import {Link, link} from "svelte-navigator";
</script>
<header class="header pt-2">
    <div class="container-fluid navigation pb-5 mb-3">
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a href="" class="navbar-brand">
                <img src="ebay.png" width="80" height="40" alt="Logo" id="logo">
            </a>

            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#toggleMobileMenu"
                    aria-controls="toggleMobileMenu" aria-expanded="false">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="navbar-collapse" id="toggleMobileMenu">
                <ul class="navbar-nav ms-auto">
                    <li><a class="nav-link" href="/" use:link>HOME</a></li>
                    <li><a class="nav-link" href="/auction" use:link>Angebote</a></li>
                    <li><a class="nav-link" href="/bid" use:link>Gebote</a></li>
                </ul>
            </div>
        </nav>
    </div>
</header>

<style>
    .navbar {
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
</style>