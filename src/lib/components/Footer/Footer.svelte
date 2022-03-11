<script context="module">
    // Libraries
    import {browser} from '$app/env'
    import {loadTranslations, t} from '$lib/translations'

    // Components
    import ColorSchemeSwitcher from '$lib/components/Switcher/ColorSchemeSwitcher.svelte'

    /** @type {import('@sveltejs/kit').Load} */
    export const load = async ({url}) => {
        const {pathname} = url
        const lang = `${pathname.match(/\w+?(?=\/|$)/) || ''}`
        const route = pathname.replace(new RegExp(`^/${lang}`), '')

        await loadTranslations(lang, route)
        return {stuff: {route, lang}}
    }
</script>

<script>
    import {page} from '$app/stores'

    $: ({route, lang} = $page.stuff)
</script>

{#if browser}
    <hr class="my-2"/>
    <footer class="d-flex flex-wrap justify-content-between">
        <div class="d-flex flex-wrap flex-row">
            <div>
                {$t(`common.copyright`)}
            </div>
        </div>
        <div class="d-flex flex-wrap flex-row">
            <div>
                {#if lang === 'en'}
                    <a class="curPoi" href={"javascript:void(1)"}
                       on:click={() => window.location.replace(`/zh${route}`)}>
                        {$t('lang.zh')}
                    </a>
                {:else}
                    <a class="curPoi" href={"javascript:void(0)"}
                       on:click={() => window.location.replace(`/en${route}`)}>
                        {$t('lang.en')}
                    </a>
                {/if}
            </div>
            <div class="ms-2">
                <ColorSchemeSwitcher />
            </div>
        </div>
    </footer>
{/if}

<style lang="scss">
  footer {
    font-size: calc(var(--bs-body-font-size) * 0.75);
  }
</style>
