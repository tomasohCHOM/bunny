<script lang="ts">
  import { T } from "@threlte/core";
  import {
    Grid,
    OrbitControls,
    TransformControls,
    useGltf,
  } from "@threlte/extras";
  import * as Three from "three";
  import { DEG2RAD } from "three/src/math/MathUtils";

  let y = 2;
</script>

<!-- Grid -->
<!-- <Grid cellColor="#808080" sectionSize={0} /> -->

<!-- Camera -->
<T.PerspectiveCamera position={[20, 20, 20]} fov={50} makeDefault>
  <!-- Controls -->
  <OrbitControls enableDamping />
</T.PerspectiveCamera>

<!-- Lights the scene equally -->
<T.AmbientLight color="#ffffff" intensity={3} />

<!-- Light that casts a shadow -->
<T.PointLight
  color="#fcffde"
  intensity={0.2}
  position={[10, 10, 0]}
  shadow.camera.top={8}
  castShadow
/>

<!-- Floor -->
<T.Mesh rotation.x={DEG2RAD * 90} receiveShadow>
  <T.PlaneGeometry args={[100000, 100000]} />
  <T.MeshStandardMaterial color="#95ed8e" side={Three.DoubleSide} />
</T.Mesh>

{#await useGltf("/assets/bunny.glb") then bunny}
  <T is={bunny.scene} position={[0, 0.5, 0]} scale={0.4} />
{/await}
