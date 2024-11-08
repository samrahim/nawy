<nav>
    <img
        alt="Nawy"
        itemprop="image"
        loading="lazy"
        width="102"
        height="50"
        decoding="async"
        data-nimg="1"
        style="color:transparent"
        src="./src/assets/nawy.png"
    />
    <ul>
        <li><a href="/" class="home-link">Home</a></li>
        <li><a href="/search" class="search-link">Search</a></li>
        <li><a href="/sell" class="sell-link">Sell</a></li>
        <li><a href="/blog" class="blog-link">Blog</a></li>
        <li><a href="/about" class="about-link">About</a></li>
        <li><a href="/contact" class="contact-link">Contact</a></li>
        <li><a href="/nawy_now" class="nawy-link">Nawy Now</a></li>
        <li><a href="/careers" class="careers-link">Careers</a></li>
    </ul>
    <h1 class="arabic">العربية</h1>
</nav>

<slot />

<style>
    .arabic {
        margin: 10px;
        color: indigo;
        font-weight: 400;
        font-size: 1.3em;
    }

    /* Font size for each link */
    .home-link {
        color: indigo;
        font-size: 1.2em;
        font-weight: 400;
    }
    .search-link {
        font-weight: 400;
        font-size: 1.1em;
    }
    .sell-link {
        font-weight: 400;
        font-size: 1.2em;
    }
    .blog-link {
        font-weight: 400;
        font-size: 1.1em;
    }
    .about-link {
        font-size: 1.1em;
        font-weight: 400;
    }
    .contact-link {
        font-size: 1.1em;
        font-weight: 400;
    }
    .nawy-link {
        font-size: 1.2em;
        font-weight: 400;
    }
    .careers-link {
        font-size: 1.1em;
        font-weight: 400;
    }

    nav {
        display: flex;
        align-items: center;
    }

    ul {
        margin-left: auto;
        display: flex;
        list-style: none;
        margin-right: auto;
    }

    ul li a {
        color: rgb(89, 88, 88);
        text-decoration: none;
    }

    li {
        margin-right: 20px;
    }

    h1 {
        margin: 0;
        font-size: 1.5em;
        font-weight: normal;
    }
</style>
