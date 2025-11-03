
<!--Delar upp sidan i två delar-->
<main>
  <div>
    <h1 class="name"> Förnamn Efternamn </h1>
    <h2>Här har jag samlat min uppgifter jag gjort i samband med webbutveckling i årskurs 2 på Maja Beskowgymnasiet!</h2>
    <h3>Inspirerade citat för min webbutvecklingsresa:</h3>
    <!--Under denna kommer vi lägga till fler element-->
  <p id="inspo">
    "The only way to learn a new programming language is by writing programs in it." - <strong>Dennis Ritchie</strong>, creator of the C programming language.
  </p>

  <p style="background-color:pink">
    "Every great developer you know got there by solving problems they were unqualified to solve until they actually did it." - <span>Patrick McKenzie, software engineer and entrepreneur</span>.
  </p>

  </div>
    <!--Här kommer vi lägga till en bild senare i uppgiften 1.2.4 Extra styling-->  

</main>\

<style>
  #inspo{
    font-family: courier;
    font-size: 160%;
  }

  span{
      color: green;
  }
  main{
    /*Styling för att dela upp sidan i två delar. */
    /*Vi kommer gå igenom detta i detalj senare*/
    margin: auto;
    width: 80vw;
    height: 70vh;
    display: grid;
    grid-template-columns: repeat(2,50%);
    overflow: hidden;
  }
  div{
    /*Styling för att centrera texten i behållaren*/
    margin: auto;
  }


    .name{
        font-family:'Gill Sans';
        font-size: 50px;
    }
    
    h1{
        color:grey;
    }
    h2{
        color: rgb(255, 165, 0);
    }
    h3{
        color: #3cb371;
        font-family: sans-serif;
        font-weight: bold;
    }
  </style>

