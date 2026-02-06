<script>
    import ElizaBot from 'elizabot'; 
    import { enhance } from "$app/forms";
    const eliza = new ElizaBot();
    let chat = $state([{ user: 'Eliza', message: eliza.getInitial(), time: getTime()}]);
    let isbottalking = $state(false);

    function clearChat() {
        chat = [
            {user: 'Eliza', message: eliza.getInitial(), time: getTime()}
        ];
    }


    function getTime() {
        const now = new Date();
        return now.toLocaleTimeString("sv-SE", {
            hour: "2-digit",
            minute: "2-digit"
        })
    }
    
    async function write(message) {
        chat = [...chat, { user: 'You', message, time:getTime() }];
        isbottalking = true;

        var element = document.getElementById("visible");
        element.style.display = "flex";   

        await new Promise((r) => setTimeout(r, 1000 + Math.random() * 1000));

        chat = [...chat, { user: 'Eliza', message: eliza.transform(message), time: getTime() }];

        element.style.display = "none";
        isbottalking = false;
    }
</script>

<main>
    <section>
        {#each chat as msg}
            <article class={msg.user === 'You' ? 'user-message' : 'eliza-message'} data-user={msg.user} data-time={msg.time}>
                <p>{msg.message}</p>
            </article>
        {/each}

        <article id="visible">
            <span class="circle"></span>
            <span class="circle"></span>
            <span class="circle"></span>
        </article>
    </section>  
    
    <form  method="post"
        use:enhance={({ formElement, formData, action, cancel }) => {
        cancel();
        const text = formData.get("text");
        write(text);

        formData.reset()

        }}>
                
        <input type="text" name="text" placeholder="Skriv ett meddelande" disabled={isbottalking}>

        <button type="button" onclick={clearChat}>
        Clear chat
        </button>

    </form>
</main>

<style>
    .user-message {
        background-color: #1976d2; 
        text-align: right;
        margin: 10px 0;
        padding: 10px;
        border-radius: 10px;
        max-width: 70%;
        align-self: flex-end;
    }

    .eliza-message {
        background-color: #1565c0; 
        text-align: left;
        margin: 10px 0;
        padding: 10px;
        border-radius: 10px;
        max-width: 70%;
        align-self: flex-start;
    }
    main {
        width: 60vw;
        height: 70vh;
        padding: 10px;
        background-color: royalblue;
        margin: auto;
        display: grid;
        grid-template-rows: 90% 10%;
        border-radius: 25px;
    }

    section {
        overflow-y: scroll;
        display: flex;
        flex-direction: column;
    }

    article {
        margin: 10px;
        padding: 10px;
        border-radius: 10px;
        width: 90%;
        background-color: #2196f3;
    } 


    input {
        width: 90%;
        height: 60%;
        margin: auto;
        background-color: #2196f3;
        border: 3px solid cornflowerblue;
        border-radius: 15px;
    }

    input:focus {
        border-color: #45AD47;
        outline: none;
        box-shadow: 0 0 0 3px rgba(49, 130, 206, 0.3);
    }

    #visible {
        display: none;
        background-color: #1565c0;
        text-align: left;
        margin: 10px 0;
        padding: 10px;
        border-radius: 10px;
        max-width: 70%;
        align-self: flex-start;
        min-height: 60px;
        align-items: center;
        gap: 10px;
    }

    .circle {
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background-color: darkblue;
        animation: typing 1000ms ease-in-out infinite;
        margin: 0 3px;
    }

    @keyframes typing {
        0% {
            transform: scale(1);
        }
        25% {
            transform: scale(1);
        }
        50% {
            transform: scale(1.4);
        }
        100% {
            transform: scale(1);
        }
    }

    .circle:nth-child(1) {
        animation-delay: 0ms;
    }
    .circle:nth-child(2) {
        animation-delay: 333ms;
    }
    .circle:nth-child(3) {
        animation-delay: 666ms;
    }

    article {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    input::placeholder{
        color: rgba(255, 255, 255, 0.6);
        font-style: italic;
    }

    article::before{
        content: attr(data-user);
        font-size: 0.8em;
        color: darkgray;
        margin-right:10px;
    }
    article::after{
        content: attr(data-time);
        font-size: 0.8em;
        color: darkgray;
        margin-left:10px;
    }

    article:hover {
        background-color: #135FAF;
        transform: scale(1.05);
    }

    article:first-child {
        background-color: #105499;
    }
</style>
