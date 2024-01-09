<script>
  import { Canvas, T } from "@threlte/core";
  import { OrbitControls, Text, useGltf } from "@threlte/extras";

  const models = {
    tv: "tv",
    car: "car",
    car2: "che",
  };

  let text = "top right deg for select ^";
  let fontSize = 2;

  let select = models[1];
</script>

<div class="app">
  <select name="models" id="models" bind:value={select}>
    {#each Object.keys(models) as key}
      <option value={models[key]}>{key}</option>
    {/each}
  </select>
  <Canvas rendererParameters={{ antialias: true }}>
    {#await useGltf(`/models/${select}.glb`) then gltf}
      <T is={gltf.scene} position.y={0.02} scale={select === "car" ? 0.1 : 1} />
    {/await}

    <Text {text} color="white" {fontSize} anchorY={-17} />

    <T.PerspectiveCamera makeDefault position={[10, 20, 40]}>
      <OrbitControls
        autoRotate={false}
        enableDamping={true}
        rotateSpeed={1}
        zoomToCursor={true}
        zoomSpeed={1}
        minPolarAngle={0}
        maxPolarAngle={Math.PI}
        enableZoom={true}
      />
    </T.PerspectiveCamera>
    <T.AmbientLight intensity={7} />
    <T.DirectionalLight position.y={20} position.z={-50} intensity={2} />

    <T.GridHelper args={[200, 100]} receiveShadow />
  </Canvas>
</div>

<style>
  .app {
    position: relative;
    height: 100%;
    width: 100%;
    background: radial-gradient(#103272, #317c7c);
  }
  select {
    position: absolute;
    margin-inline: auto;
    right: 0;
    margin: 15px;
  }
</style>
