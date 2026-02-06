<script>
    const backofcard="https://imageio.forbes.com/specials-images/imageserve/604202ff091b6539cb90fcbc/The-backs-of-a-number-of-Pok-mon-cards-/960x0.jpg?format=jpg&width=960"
     
    // Importera goto-funktionen för att navigera mellan sidor
    import { goto } from '$app/navigation';
    import { base } from '$app/paths';
  
    // Funktion som hanterar formulärets submit-händelse
    function handleSubmit(e) {
        // Förhindra att sidan laddas om (standardbeteende för formulär)
        e.preventDefault();
    
        // Skapa ett FormData-objekt från formuläret
        const formData = new FormData(e.target);
    
        // Hämta värdet från input-fältet med name="search"
        const search = formData.get('search');
    
        // Navigera till den dynamiska routen /search/[pokemon]
        goto(`${base}/search/${search}`);
    }
</script>

<main>
    <h1>Search for pokemon</h1>
    <form onsubmit={handleSubmit}>
        <input type="text" name="search" placeholder="Sök upp en pokemon" />
    </form>
    <slot></slot>
</main>

<div class="backdrop"></div>

<style>
    main{
        width: 80vw;
        height: 100vh;
        background-color: rgba(255, 255, 255, 0.8);
        margin: 5vh auto;
        border-radius: 5px;
        border: 3px;

        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .backdrop {
        width: 100vw;
        height: 100vh;
        background-image: url('https://imageio.forbes.com/specials-images/imageserve/604202ff091b6539cb90fcbc/The-backs-of-a-number-of-Pok-mon-cards-/960x0.jpg?format=jpg&width=960');
        background-size: cover;
        background-position: center;
        position: fixed;
        top: 0;
        left: 0;
        z-index: -1;
        filter: blur(5px);
    }

    input {
        border-radius: 10px;
        color: black;
        width: 50vw;
        height: 3vw;
        font-size: 20px;
    }
</style>