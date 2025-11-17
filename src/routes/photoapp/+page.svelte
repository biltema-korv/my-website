
<script>

let image = "https://picsum.photos/id/70/367/267"
let photo = "https://picsum.photos/id/88/367/267"
let picture = "https://picsum.photos/id/93/367/267"

</script>

<!--Delar upp sidan i två delar-->
<main>
  <div>
    <h1 class="flex-container"> Photoapp</h1>
    <h2 class="flex-container">Denna sida innehåller fina bilder</h2>
    <!--Under denna kommer vi lägga till fler element-->
  </div>
    <!--Här kommer vi lägga till en bild senare i uppgiften 1.2.4 Extra styling-->  
  <div class="photos">
    <img class="image-wrapper" src={image} alt="Flexbox egenskaper">
    <img class="image-wrapper" src={photo} alt="Flexbox egenskaper">
    <img class="image-wrapper" src={picture} alt="Flexbox egenskaper">
  </div>
</main>\

<style>
  main{
    /*Styling för att dela upp sidan i två delar. */
    /*Vi kommer gå igenom detta i detalj senare*/
    margin: auto;
    display: grid;
    overflow: hidden;
  }

  
  /*div{
    Styling för att centrera texten i behållaren
    margin: auto;
  }/*

  /*.text{
        font-family:'Gill Sans';
        font-size: 50px;
    }*/

    /*.text2{
        font-family:'Gill Sans';
        font-size: 30px;
    }*/
    
    h1, h2 {
      display: inline-block;
      /*Ger utrymme mellan element*/
      /*margin: 40px;*/
    }


    .flex-container {
        font-family:'Gill Sans';
        display: flex;
        flex-direction:row
    }


h1{
    text-align: center;
    font-size: 50px;
    margin: 20px;
    color: grey;
}

    .photos{
        display:flex;
        flex-wrap: nowrap;
        /*flex-direction: column;*/
        align-items:center;
        justify-content: center;
        /*Sätter att bredden på vår box enbart får
        vara 90% av webb fönstrets bredd*/
        gap: 10px;
        width: 100%;
        height: 100%;
    }

    .image-wrapper{ 
        width: 300px;
        flex: 1;
        border-radius: 20px;
        box-shadow: 4px 8px 10px rgba(0,0,0,0.2); }

    .image-wrapper:hover { flex:1.5;  }

    .image-wrapper:active { transform: scale(0.9); }
        
  </style>