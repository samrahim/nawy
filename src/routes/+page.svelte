<script lang="ts">
    import { writable } from "svelte/store";
    let selectedPrices: { min: number; max: number }[] = [];
    import Navbar from "./navebare.svelte";
    import { onMount } from "svelte";

    let viewportHeight: number;
    let isDropdownOpen = false;
    let isBedroomsdownOpen = false;
    let isPricedownOpen = false;
    const items = Array(6).fill("Child");
    const texts = [
        "",
        "Developer Units",
        "Resale Units",
        "Sell Your Units",
        "Nawy Now",
        "Offers",
        "Top Areas",
    ];
    function toggleSelection(minPrice: number, maxPrice: number) {
        const rangeIndex = selectedPrices.findIndex(
            (range) => range.min === minPrice && range.max === maxPrice,
        );

        // If range is already selected, remove it
        if (rangeIndex !== -1) {
            selectedPrices.splice(rangeIndex, 1);
        } else {
            // If range is not selected, add it
            selectedPrices.push({ min: minPrice, max: maxPrice });
        }
    }
    let val = writable("Price");

    function getPriceRange() {
        console.log(val.subscribe);

        if (selectedPrices.length === 0) return val.set("Price");
        const min = Math.min(...selectedPrices.map((range) => range.min));
        const max = Math.max(...selectedPrices.map((range) => range.max));
        console.log(`${min}M to ${max}M`);
        val.set(`${min}M to ${max}M`);
    }
    function toggleDropdown() {
        isDropdownOpen = !isDropdownOpen;
        isBedroomsdownOpen = false;
        isPricedownOpen = false;
    }
    function togglebedroomsdown() {
        isBedroomsdownOpen = !isBedroomsdownOpen;
        isDropdownOpen = false;
        isPricedownOpen = false;
    }
    function togglePricedown() {
        isPricedownOpen = !isPricedownOpen;
        isDropdownOpen = false;
        isBedroomsdownOpen = false;
    }

    function handleClickOutside(event: MouseEvent) {
        const dropdown = document.querySelector(".custom-dropdown");
        if (dropdown && !dropdown.contains(event.target as Node)) {
            isDropdownOpen = false;
        }
    }
    function handleBedroomsOutside(event: MouseEvent) {
        const dropdown = document.querySelector(".custom-bedrooms");
        if (dropdown && !dropdown.contains(event.target as Node)) {
            isBedroomsdownOpen = false;
        }
    }
    function handlePriceOutside(event: MouseEvent) {
        const dropdown = document.querySelector(".custom-price");
        if (dropdown && !dropdown.contains(event.target as Node)) {
            isPricedownOpen = false;
        }
    }

    onMount(() => {
        viewportHeight = window.innerHeight;
        document.addEventListener("click", handleClickOutside);
        document.addEventListener("click", handleBedroomsOutside);
        document.addEventListener("click", handlePriceOutside);
        return () => {
            document.removeEventListener("click", handleClickOutside);
            document.removeEventListener("click", handleBedroomsOutside);
            document.removeEventListener("click", handlePriceOutside);
        };
    });
</script>

<Navbar />

<main>
    <div class="stack-container">
        <!-- svelte-ignore a11y_img_redundant_alt -->
        <img
            src="./src/assets/landing-background.edcd0e3d.webp"
            alt="Description of the image content"
            class="stack-image"
        />

        <p class="overlay-text">Find Your New Home</p>
        <p class="overlay-text2">
            Search & compare among 5000+ properties and 500+ compounds or list
            your property for sale
        </p>
        <div class="bottom-container">
            <div class="search-bar">
                <input
                    type="text"
                    placeholder="Area, Compound, Real Estate Developer"
                    class="search-input"
                />
                <div class="custom-dropdown">
                    <!-- svelte-ignore a11y_no_static_element_interactions -->
                    <!-- svelte-ignore a11y_click_events_have_key_events -->
                    <div class="dropdown-selected" on:click={toggleDropdown}>
                        Property Types
                    </div>
                    <div
                        class="dropdown-options {isDropdownOpen ? 'open' : ''}"
                    >
                        <label class="option">
                            <input type="checkbox" /> Apartment
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Villa
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Twinhouse
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Townhouse
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Duplex
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Penthouse
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Chalet
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Office
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Clinic
                        </label>
                        <label class="option">
                            <input type="checkbox" /> Retail
                        </label>
                    </div>
                </div>
                <div class="custom-bedrooms">
                    <!-- svelte-ignore a11y_no_static_element_interactions -->
                    <!-- svelte-ignore a11y_click_events_have_key_events -->
                    <div
                        class="dropdown-bodrooms"
                        on:click={togglebedroomsdown}
                    >
                        Bedrooms
                    </div>
                    <div
                        class="dropdown-bedrooms-options {isBedroomsdownOpen
                            ? 'open'
                            : ''}"
                    >
                        <label class="option">
                            <input type="checkbox" /> 1 Bedrooms
                        </label>
                        <label class="option">
                            <input type="checkbox" /> 2 Bedrooms
                        </label>
                        <label class="option">
                            <input type="checkbox" /> 3 Bedrooms
                        </label>
                        <label class="option">
                            <input type="checkbox" /> 4 Bedrooms
                        </label>
                        <label class="option">
                            <input type="checkbox" /> 5 Bedrooms
                        </label>
                        <label class="option">
                            <input type="checkbox" /> 5 + Bedrooms
                        </label>
                    </div>
                </div>
                <div class="custom-price">
                    <!-- svelte-ignore a11y_no_static_element_interactions -->
                    <!-- svelte-ignore a11y_click_events_have_key_events -->
                    <div class="dropdown-price" on:click={togglePricedown}>
                        {$val}
                    </div>
                    <div
                        class="dropdown-price-options {isPricedownOpen
                            ? 'open'
                            : ''}"
                    >
                        <label class="option">
                            <input
                                type="checkbox"
                                on:change={() => {
                                    toggleSelection(1, 4), getPriceRange();
                                }}
                            /> 1M To 4M
                        </label>
                        <label class="option">
                            <input
                                type="checkbox"
                                on:change={() => {
                                    toggleSelection(4, 10), getPriceRange();
                                }}
                            /> 4M To 10M
                        </label>
                        <label class="option">
                            <input
                                type="checkbox"
                                on:change={() => {
                                    toggleSelection(10, 15), getPriceRange();
                                }}
                            /> 10M To 15M
                        </label>
                        <label class="option">
                            <input
                                type="checkbox"
                                on:change={() => {
                                    toggleSelection(15, 30), getPriceRange();
                                }}
                            /> 15M To 30M
                        </label>
                        <label class="option">
                            <input
                                type="checkbox"
                                on:change={() => {
                                    toggleSelection(30, 50), getPriceRange();
                                }}
                            /> 30M To 50M
                        </label>
                        <label class="option">
                            <input
                                type="checkbox"
                                on:change={() => {
                                    toggleSelection(50, 100), getPriceRange();
                                }}
                            /> 50M To 100M
                        </label>
                    </div>
                </div>
                <button class="search-button">Search</button>
            </div>
        </div>
    </div>
    <h1 class="What-are">What Are You Looking For ?</h1>
    <div class="p">
        <div class="grid-container">
            {#each items as _, index}
                <div class="grid-item">
                    <img
                        src={`./src/assets/medium${index + 1}.webp`}
                        alt={`Image ${index + 1}`}
                    />
                    <p class="image-text">{texts[index + 1]}</p>
                </div>
            {/each}
        </div>
    </div>
</main>

<style>
    .p {
        padding-left: 30px;
        padding-right: 30px;
    }
    .What-are {
        padding-top: 0%;
        padding-left: 30px;
        color: indigo;
        font-size: 30px;
        font-weight: bold;
    }
    .custom-dropdown,
    .custom-bedrooms,
    .custom-price {
        position: relative;
        width: 200px;
        font-family: Arial, sans-serif;
    }

    .dropdown-selected,
    .dropdown-price,
    .dropdown-bodrooms {
        padding: 15px;
        border: 1px solid #ddd;
        border-radius: 8px;
        background-color: #fff;
        cursor: pointer;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .dropdown-bedrooms-options,
    .dropdown-price-options,
    .dropdown-options {
        display: none; /* Hidden by default */
        position: absolute;
        top: 100%;

        width: 100%;
        max-height: 150px;
        overflow-y: auto;
        border: 1px solid #ddd;
        border-radius: 8px;
        background-color: #fff;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        z-index: 10;
        padding: 15px;
        box-sizing: border-box;
    }

    .dropdown-options.open,
    .dropdown-bedrooms-options.open,
    .dropdown-price-options.open {
        display: block; /* Show the dropdown if it's open */
    }

    .option {
        display: flex;
        align-items: center;
        padding: 5px 0;
        cursor: pointer;
    }

    .option input[type="checkbox"] {
        margin-right: 10px;
    }

    .option:hover {
        background-color: #f0f0f0;
    }

    .stack-container {
        padding-top: 10px;
        position: relative;
        width: 100%;
        height: 50vh;
    }

    .stack-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
        filter: grayscale(40%);
        color: transparent;
    }

    .overlay-text {
        position: absolute;
        top: 10px;
        left: 20px;
        color: white;
        font-weight: bold;
        font-size: 4em;
        z-index: 1;
    }

    .overlay-text2 {
        position: absolute;
        top: 120px;
        left: 20px;
        color: white;
        font-weight: 600;
        font-size: 1.5em;
        z-index: 1;
    }

    .bottom-container {
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
        width: 85vw;
        background-color: rgba(255, 255, 255, 0.8);
        padding-top: 20px;
        padding-bottom: 20px;
        margin-block-end: 10px;
        border-radius: 12px;
        display: flex;
        justify-content: space-evenly;
        z-index: 1;
    }

    .search-bar {
        display: flex;
        gap: 6px;
        align-items: center;
        width: 100%;
        max-width: 1000px;
    }

    .search-input {
        flex: 2;
        padding-top: 15px;
        padding-bottom: 15px;
        border: 1px solid #ddd;
        border-radius: 8px;
        font-size: 1em;
        background-color: #fff;
        outline: invert;
    }
    .grid-container {
        display: grid;
        grid-template-columns: repeat(6, 1fr); /* 6 equal-width columns */
        gap: 10px; /* space between items */
    }

    .search-button {
        flex: 0.5;
        padding: 15px;
        border: none;
        border-radius: 8px;
        background-color: #1a3d5d;
        color: white;
        font-size: 1.2em;
        font-weight: bold;
        cursor: pointer;
        outline: none;
    }

    .search-button:hover {
        background-color: #16324c;
    }
    .grid-container {
        display: grid;
        grid-template-columns: repeat(6, 1fr); /* 6 equal-width columns */
        gap: 15px; /* Space between the items */
        width: 100%; /* Ensure the grid container does not overflow */
        overflow: hidden;
    }

    .grid-item {
        flex-direction: column;
        border: 2px solid #ccc; /* Gray border */
        border-radius: 8px; /* Optional: rounded corners */
        padding: 5px; /* Space between the border and the image */
        background-color: white; /* Optional: background color */
        align-items: center;
        justify-content: center;
        display: flex;
    }

    .grid-item img {
        width: 40px; /* Make each image fill its grid cell */
        height: 40px; /* Ensures full height coverage of each cell */
        object-fit: cover; /* Cover the entire cell without stretching */
        border-radius: 6px; /* Match the inner border radius for a seamless look */
    }

    /* Responsive behavior to handle different screen sizes */
    @media (max-width: 768px) {
        .grid-container {
            grid-template-columns: repeat(
                3,
                1fr
            ); /* 3 columns on medium screens */
        }
    }

    @media (max-width: 480px) {
        .grid-container {
            grid-template-columns: repeat(
                2,
                1fr
            ); /* 2 columns on small screens */
        }
    }
</style>
