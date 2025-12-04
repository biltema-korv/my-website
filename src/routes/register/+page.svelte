<script>

    import {users_store} from "$lib/user";
    let users = [];
    //alert(users_store)

    let color = "black"
    let name=""
    let epost=""
    let password=""
    import { onMount } from 'svelte';
    onMount(() => {
        if($users_store.length > 2){
            users = JSON.parse($users_store);
        }
    });
    function handleSubmit(){
        let new_user = {username: name, password: password, email: epost, color: color};

        let found=false
        for (let user of users) {
            if (user.username === new_user.username) {
                alert("Användarnamnet används redan.")
                found=true
                break
            }
        }

        if (!found){
            users = [...users,new_user];
            $users_store = users;
            alert(`Välkommen ${name}, din epost adress är ${epost} och ditt lösenord är ${password}!`)
        }
    }
    let colors = [
        { namn: "Blå", value: "blue" },
        { namn: "Röd", value: "red" },
        { namn: "Grön", value: "green" },
        { namn: "Gul", value: "yellow" },
        { namn: "Rosa", value: "pink" },
        { namn: "Orange", value: "orange" },
        { namn: "Turkos", value: "cyan" },
    ]

</script>

<main>
    <div class="container">
        <form on:submit|preventDefault={handleSubmit}>
            <h1 class="flexbox">Registrering</h1>

            <div style="width: 100px; height: 100px; border-radius: 50%; overflow:hidden; background-color:{color};"></div>

            <label for="name">Namn:</label>
            <input type="text" bind:value={name}>
            <br>

            <label for="password">Lösenord:</label>
            <input type="password" bind:value={password}>
            <br>

            <label for="email">E-post:</label>
            <input type="email" bind:value={epost}>
            <br>

            <label for="color">Favoritfärg</label>
            <select id="color" bind:value={color}>
                {#each colors as c}
                    <option value={c.value}>{c.namn}</option>
                {/each}
            </select>
            <br>
            <input type="submit" value="Registrera">
            <nav>
                <a href="/login">Har redan ett konto? Logga in här</a>
            </nav>
        </form>
    </div>  
</main>

<style>
    main{
        background-image: url("https://t4.ftcdn.net/jpg/05/21/65/59/360_F_521655929_N80d5GaCQJ2VP073PfTXJTe9mkvsNtHE.jpg");
        background-size: cover;
        background-repeat: Cover;
        width: 100%;
        height: 100%;
        margin: 0%;
        padding: 0%;
        min-height: 510px;
    }

    .container{
        border: solid 5px rosybrown;
        border-radius: 10px;
        width: 35%;
        height: 80%;
        background-color: #3a2e3b;
        margin: auto;
        min-width: 300px;
        min-height: 490px;
        flex-direction: column;
        text-align: center;
        flex-grow: space-evenly;
        display: flex;
    }     

    .flexbox{
        flex-direction: column;
        text-align: center;
        flex-grow: space-evenly;
    }
        
</style>