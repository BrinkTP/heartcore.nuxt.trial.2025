<template>
    <header>
        <div class="hero-image">
            <div class="hero-text">
                <nav>
                    <ul>
                        <li>
                            <NuxtLink to="/">Home</NuxtLink>
                        </li>
                        <li>
                            <NuxtLink to="/posts/1">Post 1</NuxtLink>
                        </li>
                        <li>
                            <NuxtLink to="/posts/2">Post 2</NuxtLink>
                        </li>
                    </ul>
                </nav>
            </div>
        </div>
        <slot />
    </header>
</template>
<style>
/* The hero image */
.hero-image {
    /* Use "linear-gradient" to add a darken background effect to the image (photographer.jpg). This will make the text easier to read */
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("https://static.vecteezy.com/system/resources/previews/000/701/690/non_2x/abstract-polygonal-banner-background-vector.jpg");

    /* Set a specific height */
    height: 300px;

    /* Position and center the image to scale nicely on all screens */
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;
}

/* Place text in the middle of the image */
.hero-text {
    text-align: center;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
}
</style>