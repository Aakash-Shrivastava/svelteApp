<script>
  let name = "";
  let count = 0;

  function handleClick() {
    count += 1;
  }
</script>

<style>
  .main {
    width: 100%;
    height: 100px;
    margin: 0 auto;
    /* display: flex; */
    align-items: center;
    flex-direction: column;
    margin-top: 50px;
  }
  .header {
    font-size: 30px;
    font-weight: 800;
  }
  input {
    width: 100%;
    height: 50px;
    padding: 10px;
  }
  .main-header{
    text-align: initial;
    line-height: 39px;
  }
  .sub-header{
    margin-top: 16px;
    text-align: initial;
    line-height: 24px;
    color: #545353;
    margin-bottom: 20px;
    letter-spacing: 0.2px;
  }
  
  /* @media (min-width: 640px) {
    main {
      max-width: none;
    }
  } */
</style>

<div class="main">

  <div class="main-header">
    <div class="header">Travel like your</div>
    <div class="header">favorite influencer</div>
  </div>
  <div class="sub-header">
    <div class="subheader">Enter the handle of the favorite profile and we will find the best flight recommendations</div>
  </div>

  <input bind:value={name} placeholder="@username" />
  <!-- <button on:click={handleClick}>Search</button> -->
</div>
