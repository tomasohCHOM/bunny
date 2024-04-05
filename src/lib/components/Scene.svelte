<script lang="ts">
  import { T } from "@threlte/core";
  import { OrbitControls, useGltf } from "@threlte/extras";
  import * as Three from "three";
</script>

<!-- Camera -->
<T.PerspectiveCamera position={[8, 8, 8]} fov={70} makeDefault>
  <!-- Controls -->
  <OrbitControls enableRotate={false} minDistance={5} maxDistance={20} />
</T.PerspectiveCamera>

<!-- Lights the scene equally -->
<T.AmbientLight color="#fefff5" intensity={1} />

<!-- Light that casts a shadow -->
<T.DirectionalLight
  color="#fcffde"
  intensity={2}
  position={[20, 20, 10]}
  castShadow
/>

<!-- Floor -->
<T.Mesh rotation.x={Math.PI / 2} receiveShadow>
  <T.PlaneGeometry args={[100000, 100000]} />
  <T.MeshStandardMaterial color="#95ed8e" side={Three.DoubleSide} />
</T.Mesh>

{#await useGltf("/assets/bunny.glb") then bunny}
  <T is={bunny.scene} position={[0, 0.5, 0]} scale={0.5} />
{/await}

{#await useGltf("/assets/purple-grass.glb") then purpleGrass}
  <T is={purpleGrass.scene} position={[-10, 0.5, 0]} scale={4} />
{/await}

{#await useGltf("/assets/tree.glb") then tree}
  <T is={tree.scene} position={[10, 0.5, -4]} scale={2} />
{/await}
