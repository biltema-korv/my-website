<script>
    let varor=$state([{ name:"Mjölk", purchased: false}]);
    let tobuy=$state("")

    function handleSubmit(which){
        if(tobuy.length === 0){
            return;
            console.log("AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA");
        }

        varor.push({
            name: which,
            purchased: false
        });

        console.log("AbAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA")
    }

    function remove(which){
        const index = varor.indexOf(which);

        if (index !== -1) {
            varor.splice(index, 1); 
            console.log("Removed:", which.name);
            console.log(varor)
        }
    }
    
    function purchased(which){
        which.purchased=!which.purchased
    }
</script>


<main class="container">

    <h1>Shoppinglist</h1>
    <div class="categories_container">
        <section>
            <h2>Varor att köpa</h2>
                <div class="empty">
                    <ul>
                        {#each varor.filter(v => !v.purchased) as vara}
                            <li>
                                { vara.name }
                                <button onclick={() => remove(vara)}>Ta bort</button>
                                <button onclick={() => purchased(vara)}>Flytta till köpta</button>
                            </li>
                        {/each }
                    </ul>
                </div>
                <label for="Purchased">Lägg till varor att köpa:</label>
            <input type="text" bind:value={tobuy}>
            <br>

            <button onclick={() => handleSubmit(tobuy)}>Att köpa</button>
        </section>
        
        <section>
            <h2>Köpta varor</h2>
                <div class="mt">
                    <ul>
                        {#each varor.filter(v => v.purchased) as vara}
                            <li>
                                { vara.name }
                                <button onclick={() => remove(vara)}>Ta bort</button>
                                <button onclick={() => purchased(vara)}>Flytta till varor att köpa</button>
                            </li>
                        {/each }
                    </ul> 
                </div>
        </section>
    </div>
</main>

<style>
    .container{
        background-color: #4a412a;
        width: 60vw;
        height: 55vh;
        border-radius: 20px;
        display: grid;
        grid-template-rows: 1fr;
        margin: auto;
        padding: 20px 0;
    }

    .container > h1{
        background-color: #9aae07;
        grid-template-rows: 8fr;
        text-align: center;
        margin: 0;
    }

    .categories_container{
        background-color: #9aae07;
        width: 100%;
        display:flex;
        height: 50vh;
    }

    .empty{
        background-color: rgba(0, 0, 0, 0.1); /* svart bakgrund med 10% opacitet */
        width: 100%;
        display:flex;
        height: 40vh;
        text-align: left;
        overflow-y: auto;
    }

    .mt{
        background-color: rgba(0, 0, 0, 0.2); /* svart bakgrund med 10% opacitet */
        width: 100%;
        display:flex;
        height: 40vh;
        text-align: left;
        overflow-y: auto;
    }

    .categories_container section:first-child{  /* vilket barn vill vi styla? */
        background-color: rgba(0, 0, 0, 0.1); /* svart bakgrund med 10% opacitet */
        text-align: center;
        font-size: 20px;
        width: 50%;
        height: 10vh;
    }
 
    .categories_container section:nth-child(2){  /* vilket barn vill vi styla? */
        background-color: rgba(0, 0, 0, 0.3); /* svart bakgrund med 30% opacitet */
        text-align: center;
        font-size: 20px;
        width: 50%;
        height: 10vh;
    }
</style>