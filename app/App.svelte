<script context="module">
  // Dependencies
  import { fetch } from "tns-core-modules/fetch";

  export async function preload(page, session) {
    const testJson = ["One", "Two", "Three"];
    return testJson;
    //const url = "https://reporganizer.herokuapp.com/api/repos";
    // let result = await fetch(url);
    //return repos;
  }
</script>

<script>
  //import { fetch } from "tns-core-modules/fetch";

  export let testJson;

  // const testJson = ["One", "Two", "Three"];
  // const test = "Yo!";
  const test2 = testJson[1];

  //export let repos;
  //const url = "https://reporganizer.herokuapp.com/api/repos";

  //   async function responseOrDie(url) {
  //     let response = await fetch(url);
  //     console.log(response);

  //     return response;
  //   }

  //let repos = responseOrDie(url);

  //let testJson1;

  //   $: testJson1 = testJson[0];

  let counter = 42;
  let message;
  let message2;
  $: message =
    counter <= 0
      ? "Hoorraaay! You unlocked the Svelte-Native clicker achievement!"
      : `${counter} taps left`;

  const onTap = () => counter--;

  async function getRepos() {
    // let result = await responseOrDie(url);
    // const url = "https://reporganizer.herokuapp.com/api/repos";

    // let result = await fetch(url);
    // console.log("Result", result);
    //message2 = result[0].name;
    console.log("Inside getRepos 2!!");
    // message2 = result.length;
    //message2 = repos.length;
    message2 = test2;
  }
</script>

<page>
  <actionBar title="My App Demo 23" icon="" />
  <stackLayout class="p-20">
    <label text="Tap the button" class="h1 text-center" />
    <button text="TAP" on:tap={onTap} class="-primary -active" />
    <label text={message} class="h2 text-center" textWrap="true" />
    <!-- <label text={test2} class="h2 text-center" textWrap="true" /> -->

    <!-- {#each repos as item}
      <label text={item.name} class="h2 text-center" textWrap="true" />
    {/each} -->

    <button text="Get Repos" on:tap={getRepos} class="-primary -active" />
    <label text={message2} class="h2 text-center" textWrap="true" />

  </stackLayout>
</page>
