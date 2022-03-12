<script>
    import {onMount} from "svelte";
    import {t} from '$lib/translations'
    import {page} from '$app/stores'

    $: ({route, lang} = $page.stuff)

    const mapping = {
        en: 'zh',
        zh: 'en'
    }
    let toLang

    const switchLocale = () => {
        window.location.replace(`/${toLang}${route}`)
    }

    onMount(async () => {
        toLang = mapping[lang]
    })
</script>

<a class="curPoi" href={"javascript:void(0)"} on:click={switchLocale}>
    {$t(`lang.${toLang}`)}
</a>
