<script setup>
import MainHeader from '@blocks/MainHeader.vue'
import SideNavigation from '@blocks/SideNavigation.vue'
</script>

<template>
    <MainHeader
        v-if="$route.name !== 'auth'"
        class="header">
    </MainHeader>
    <main
        class="main"
        :class="{ container: $route.name !== 'auth' }">
        <SideNavigation
            v-if="$route.name !== 'auth'"
            class="main__side-navigation" />
        <slot />
    </main>
</template>

<style lang="scss">
$header-height: 48px;

/* stylelint-disable-next-line selector-max-id */
#app {
    display: flex;
    flex-direction: column;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
    background-color: var(--main-bg);

    /* stylelint-disable-next-line selector-max-id */
    > header {
        z-index: 20;
        min-height: 48px;
    }

    /* stylelint-disable-next-line selector-max-id */
    > main {
        position: relative;
        display: flex;
        flex-grow: 1;
        box-shadow: 0 4px 8px 0 rgb(34 60 80 / 0.1);
    }
}

.main {
    &__side-navigation {
        position: fixed;
        top: $header-height;
        left: 0;
        display: flex;
        width: 100%;
        height: calc(100vh - $header-height);
        opacity: 0;
        transition: 0.3s ease-out;
        transition-property: transform, opacity;
        transform: translateY(-100%);

        @media (min-width: 768px) {
            width: 240px;
            opacity: 1;
            transform: translateY(0) translateX(-100%);
        }

        @media (min-width: 1024px) {
            position: sticky;
            top: $header-height;
            transform: translateX(0);
        }

        &.expanded {
            opacity: 1;
            transform: translateY(0);

            @media (min-width: 768px) {
                transform: translateX(0);
            }
        }
    }
}
</style>
