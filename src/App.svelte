<script>
  import purpleair from "purpleair";
  import Dot from "./Dot.svelte";
  import { interpolateRgbBasis } from "d3-interpolate";
  import { aqanduAQIFromPM } from "./aqicalc";

  // const getStats = (async () => {
  //   const response = await fetch("purple.json");
  //   let data = await response.json();
  //   let stats = {
  //     prev: JSON.parse(data["results"][0]["Stats"]),
  //     aqi: aqanduAQIFromPM(data["results"][0]["PM2_5Value"])
  //   };
  //   console.log(stats);
  // })();

  const purple = (async () => {
    //closer one
    //hill dr 56109
    var sensor = await purpleair.getSensor(56109);
    var aqi = await purpleair.getAQI(sensor);
    var aqiClass = await purpleair.getAQIClass(aqi);
    // var stats = await purple.getAQIStats();

    // console.log(aqi);
    let data = {
      aqi: await purpleair.getAQI(sensor),
      aqiClass: await purpleair.getAQIClass(aqi),
      stats: await purpleair.getAQIStats(sensor)
    };

    // console.log(data);

    return await data;
  })();

  let getAQIcolor = function(c) {
    let color = interpolateRgbBasis([
      "green",
      "yellow",
      "orange",
      "red",
      "purple",
      "purple",
      "maroon",
      "maroon",
      "maroon",
      "maroon"
    ])(c / 500);
    return color;
  };
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  .flex-container {
    display: flex;
  }
  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <!-- {#await getStats}
    <p>..wait</p>
  {:then stats}
    {stats}
  {/await} -->

  {#await purple}
    <p>...waiting</p>
  {:then data}
    <big>
      <Dot aqi={data.aqi} />
    </big>

    <div class="flex-container">
      {#each data.stats as stat}
        <Dot aqi={aqanduAQIFromPM(stat.val)} />
      {/each}
    </div>

  {:catch error}
    <p>error</p>
  {/await}
</main>
