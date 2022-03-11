<script>
    // Components
    import Navbar from '$lib/components/Navbar/Navbar.svelte';

    // Libraries
    import {locale, t} from '$lib/translations';
</script>
<div class="container">
    <Navbar/>
    <div class="my-5">
        <h1>{$t('home.welcome')}</h1>
    </div>
</div>
