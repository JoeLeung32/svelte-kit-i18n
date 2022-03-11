<script context="module">
    // Libraries
    import {browser} from '$app/env'
    import {loadTranslations, t} from '$lib/translations'
    import {ClassColorScheme, ColorScheme} from "$lib/shares/js/ClassColorScheme/ClassColorScheme"

    let colorScheme

    /** @type {import('@sveltejs/kit').Load} */
    export const load = async ({url}) => {
        const {pathname} = url
        const lang = `${pathname.match(/\w+?(?=\/|$)/) || ''}`
        const route = pathname.replace(new RegExp(`^/${lang}`), '')

        if (colorScheme) {
            colorScheme.watch()
        }

        await loadTranslations(lang, route)
        return {stuff: {route, lang}}
    }
</script>

<script>
    import {onMount} from "svelte";
    import {writable} from 'svelte/store'
    import {page} from '$app/stores'

    $: ({route, lang} = $page.stuff)

    const funcColorScheme = {
        title: writable(0),
        switch: () => {
            if (!colorScheme) return
            colorScheme.switch()
            funcColorScheme.updateTitle()
        },
        updateTitle: () => {
            if (!colorScheme) return
            if (colorScheme.get() === ColorScheme.DARK.description) {
                funcColorScheme.$title = ColorScheme.LIGHT.description
            } else {
                funcColorScheme.$title = ColorScheme.DARK.description
            }
        }
    }
    funcColorScheme.updateTitle()

    onMount(async () => {
        colorScheme = new ClassColorScheme()
    })
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
                <span class="curPoi notSel" title={$t(`common.colorScheme.${funcColorScheme.$title}`)}
                      on:click={() => funcColorScheme.switch()}>
                    <i class="fa-solid fa-circle-half-stroke"></i>
                </span>
            </div>
        </div>
    </footer>
{/if}

<style lang="scss">
  footer {
    font-size: calc(var(--bs-body-font-size) * 0.75);
  }
</style>
