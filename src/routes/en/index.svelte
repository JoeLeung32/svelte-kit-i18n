<script>
    // Components
    import Navbar from '$lib/components/Navbar/Navbar.svelte';

    // Libraries
    import {locale, t} from '$lib/translations';
    import {marked} from 'marked';
</script>
<div class="container">
    <Navbar/>
    <div class="my-5">
        <h1>{$t('home.welcome')}</h1>
        <p>{@html marked(`Content sampling in **marked** library.`)}</p>
    </div>
</div>
