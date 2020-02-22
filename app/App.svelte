<script context="module">
  // Dependencies
  //import { fetch } from "tns-core-modules/fetch";
  // Create the Observable Module, listen for changes on the home page
  const observableModule = require("tns-core-modules/data/observable")
    .Observable;

  // Get the application module
  const application = require("tns-core-modules/application");

  // Create the new viewModel, will listen to the home page
  const viewModel = new observableModule();

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
  //  Set the Modules

  // Preferences page loads - Use Load because Navigate to only happens once, loaded happens each time you go to the page
  function onPageLoaded(args) {
    console.log("Preferences - On Loaded");

    // Declare the Page Object
    const page = args.object;

    //const getRepoBtn = page.getViewById("btnRepos");

    //const page = args.object;
    const getRepoBtn = page.getViewById("lblTest");

    let makeInvis = false;

    if (makeInvis) {
      console.log(makeInvis);

      getRepoBtn.visibility = "collapsed";
    }
  }

  // Declare variable to hold repos
  let repos;

  // let message;

  async function getRepos() {
    console.log("Inside getRepos!!");

    // API Call
    httpModule.getJSON("https://reporganizer.herokuapp.com/api/repos").then(
      r => {
        repos = r;
        // return { repos };
        // console.log(r);
        // let test = document.getElementById("btnRepos");
        // let test = Button.getViewById("btnRepos");
        // test.text = "Hi!";
      },
      e => {
        console.log("Error getting Repos", e);
      }
    );
  }

  function makeInvis(args) {
    const page = args.object;
    const getRepoBtn = page.getViewById("btnRepos");
    getRepoBtn.visibility = "collapsed";
    console.log("Invisible");
  }

  //getRepos();
</script>

<page
  xmlns="http://schemas.nativescript.org/tns.xsd"
  loaded="onPageLoaded"
  class="page">
  <actionBar title="Liberamed Demo" icon="" />
  <stackLayout class="p-20">
    <label id="lblTest" text="Tap to Get Repos" class="h1 text-center" />

    <button
      id="btnRepos"
      text="Get Repos"
      on:tap={getRepos}
      class="-primary -active" />

    <!-- <button text="Make hidden" on:tap={makeInvis} class="-primary" /> -->

    {#if repos}
      {#each repos as item}
        <label text={item.name} class="h2 text-center" textWrap="true" />
      {/each}
    {:else}
      <label text="No Repos" class="h2 text-center" textWrap="true" />
    {/if}

  </stackLayout>
</page>
