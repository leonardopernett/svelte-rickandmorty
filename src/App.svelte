

<script>
import './app.css'
import Character from "./libs/Character.svelte"
 
  let characters = []
  let page = 1
   async function loadCharacter(){
     const resp = await fetch('https://rickandmortyapi.com/api/character?page='+page)
     const { results } = await resp.json()
     characters = results
   }

   loadCharacter()

   function next(){
     page ++
     loadCharacter()
   }
   function back(){
    if(page ==1){
      return
    }
     page --
     loadCharacter()
   }
</script>

<h1 class="title">rick and morty svelte</h1>
<div class="container">
 
  <div class="btns">
    <button disabled={page==1}  on:click={back}>previous</button>
    <button  on:click={next}>next</button>
  
  </div>
  <div class="grid">
    {#each characters as character }
       <Character character={character} />
    {/each}
  </div>
</div>
 

