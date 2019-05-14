<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light mb-5">
        <nuxt-link :to="{name: 'index'}" class="navbar-brand">Zou</nuxt-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item active">
                    <nuxt-link :to="{name: 'index'}" class="nav-link">Home</nuxt-link>
                </li>
                <li class="nav-item active">
                    <nuxt-link :to="{name: 'blog'}" class="nav-link">Blog</nuxt-link>
                </li>
            </ul>
        </div>
    </nav>
</template>
