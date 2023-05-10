<script setup>
import { RouterLink } from 'vue-router';
</script>
<template>
    <header>
        <div class="header_container">
            <div class="branding_container">
                <div class="branding_logo">
                    <img src="@/logo.svg" alt="logo" />
                </div>
                <div class="branding_name">Vue Todos</div>
            </div>
            <nav>
                <RouterLink :to="{ name: 'home' }">Home</RouterLink>
                <RouterLink :to="{ name: 'about' }">About</RouterLink>
            </nav>
        </div>
    </header>
</template>

<style lang="scss" scoped>
header {
    background-color: #c7f9cc;
    padding: 25px 16px;
    .header_container {
        max-width: 90vw;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-left: auto;
        margin-right: auto;
    }
    .branding_container {
        display: flex;
        align-items: center;
        .branding_logo {
            width: 45px;
            height: 45px;
            padding-right: 0.7rem;
        }
        .branding_name {
            font-size: 24px;
            font-weight: bold;
            color: #7fa9d3;
        }
    }
    nav {
        a {
            color: #7fa9d3;
            text-decoration: none;
            padding-bottom: 0.3rem;

            &:nth-child(2) {
                margin-left: 1rem;
            }
            &.router-link-active {
                border-bottom: solid 2px #7fa9d3;
            }
        }
    }
}
</style>
