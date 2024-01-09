<script>
  import { Canvas, T } from "@threlte/core";
  import { GLTF, OrbitControls } from "@threlte/extras";
</script>

<div class="app">
  <Canvas rendererParameters={{ antialias: true }}>
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
    <GLTF url="/car.glb" position.y={0.02} scale={0.1} />
    <T.GridHelper args={[200, 100]} />
  </Canvas>
</div>

<style>
  .app {
    position: absolute;
    height: 100%;
    width: 100%;
    background: radial-gradient(#103272, #317c7c);
  }
</style>
