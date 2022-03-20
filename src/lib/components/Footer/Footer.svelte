<script>
    // Libraries
    import {browser} from '$app/env'
    import {t} from '$lib/translations'

    // Components
    import ColorSchemeSwitcher from '$lib/components/Switcher/ColorSchemeSwitcher.svelte'
    import LocaleSwitcher from '$lib/components/Switcher/LocaleSwitcher.svelte'
</script>

{#if browser}
    <hr class="my-2"/>
    <footer class="d-flex flex-wrap justify-content-between">
        <div class="d-flex flex-wrap flex-row">
            <div>
                {$t(`common.copyright`, {
                    crYear: new Date().getFullYear()
                })}
            </div>
        </div>
        <div class="d-flex flex-wrap flex-row">
            <div>
                <ColorSchemeSwitcher/>
            </div>
            <div class="ms-2">
                <LocaleSwitcher/>
            </div>
        </div>
    </footer>
{/if}

<style lang="scss">
  footer {
    font-size: calc(var(--bs-body-font-size) * 0.75);
  }
</style>
