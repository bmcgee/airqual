<script>
  import Dot from "./Dot.svelte";
  import {
    aqiUpOrDown,
    aqanduAQIFromPM,
    getAQIDescription,
    aqiStatParse,
    aqiColorParse,
    getAQIMessage
  } from "./aqicalc";
  import aqi from "purpleair";
  import { validate_component } from "svelte/internal";

  //hill dr 56109

  const sensorData = (async () => {
    const response = await fetch("https://www.purpleair.com/json?show=56109");
    const json = await response.json();
    const pm = await json["results"][0]["PM2_5Value"];
    const stats = await JSON.parse(json["results"][0]["Stats"]);
    let data = await {
      aqi: aqanduAQIFromPM(pm),
      previous: aqiStatParse(stats)
    };
    console.log(data);
    return await data;
  })();
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    font-family: monospace;
  }

  .flex-container {
    display: flex;
  }
  .sub {
    width: 100%;
  }
  @media only screen and (min-width: 768px) {
    main {
      width: 50%;
    }
  }
</style>

<main>
  {#await sensorData}
    <p>...waiting</p>
  {:then data}
    <big>
      <Dot aqi={data.aqi} time="Now" />
      <p>{getAQIDescription(data.aqi)}</p>
      <p>{getAQIMessage(data.aqi)}</p>

    </big>

    <div class="flex-container">
      {#each Object.entries(data.previous) as [time, val]}
        <div class="sub">
          <Dot aqi={aqanduAQIFromPM(val)} />
          <p
            style="height: auto; background-color: {aqiUpOrDown(data.aqi, aqanduAQIFromPM(val))}">
            {time}
          </p>
        </div>
      {/each}
    </div>

  {:catch error}
    <p>error</p>
  {/await}
</main>
