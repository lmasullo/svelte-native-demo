<script context="module">
  // Dependencies
  //import { fetch } from "tns-core-modules/fetch";
  const httpModule = require("tns-core-modules/http");

  export async function preload() {
    // httpModule.getJSON("https://reporganizer.herokuapp.com/api/repos").then(
    //   r => {
    //     console.log(r);
    //     repos = r;
    //     return { repos };
    //   },
    //   e => {
    //     console.log("Error getting Repos", e);
    //   }
    // );
  }
</script>

<script>
  // Declare variable to hold repos
  let repos;

  // let message;

  async function getRepos() {
    console.log("Inside getRepos!!");

    // API Call
    httpModule.getJSON("https://reporganizer.herokuapp.com/api/repos").then(
      r => {
        repos = r;
        //return { repos };
        //console.log(r);
        //let test = document.getElementById("btnRepos");
        let test = Button.getViewById("btnRepos");
        test.text = "Hi!";
      },
      e => {
        console.log("Error getting Repos", e);
      }
    );
  }

  function makeInvis(args) {
    //let test = Button.getViewById("btnRepos");
    //test.text = "Hi!";
    const page = args.object;
    let sl = page.getViewById("btnRepos");
    sl.visibility = "collapsed";
  }

  //getRepos();
</script>

<page>
  <actionBar title="Liberamed Demo" icon="" />
  <stackLayout class="p-20">
    <label text="Tap to Get Repos" class="h1 text-center" />

    <!-- <label text={message} class="h2 text-center" textWrap="true" /> -->

    <button
      id="btnRepos"
      text="Get Repos"
      on:tap={getRepos}
      class="-primary -active" />

    <button text="Make hidden" on:tap={makeInvis} class="-primary" />

    {#if repos}
      {#each repos as item}
        <label text={item.name} class="h2 text-center" textWrap="true" />
      {/each}
    {:else}
      <label text="No Repos" class="h2 text-center" textWrap="true" />
    {/if}

  </stackLayout>
</page>
