<template>
    <nav class="navbar navbar-expand-lg navbar-light fixed-top" id="mainNav">
        <div class="container">
            <nuxt-link :to="{name: 'index'}" class="navbar-brand">Start Bootstrap</nuxt-link>
            <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
                Menu
                <i class="fas fa-bars"></i>
            </button>
            <div class="collapse navbar-collapse" id="navbarResponsive">
                <ul class="navbar-nav ml-auto">
                    <li class="nav-item">
                        <nuxt-link :to="{name: 'index'}" class="nav-link">Home</nuxt-link>
                    </li>
                    <li class="nav-item">
                        <nuxt-link :to="{name: 'blog'}" class="nav-link">Blog</nuxt-link>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>
