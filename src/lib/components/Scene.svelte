<script lang="ts">
  import { T } from "@threlte/core";
  import { OrbitControls, useGltf } from "@threlte/extras";
  import * as Three from "three";

  const GRASS_BOUNDARY = 10;
  const TREE_BOUNDARY = 7;

  function getRandom(boundary: number) {
    let min = -1 * boundary;
    let max = boundary;
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }

  let grassPositions = Array.from({ length: 10 }, () => [
    getRandom(GRASS_BOUNDARY),
    0.5,
    getRandom(GRASS_BOUNDARY),
  ]);
  let treePositions = Array.from({ length: 2 }, () => [
    getRandom(TREE_BOUNDARY),
    0.5,
    getRandom(TREE_BOUNDARY),
  ]);
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

{#each grassPositions as grassPosition}
  {#await useGltf("/assets/purple-grass.glb") then purpleGrass}
    <T is={purpleGrass.scene.clone()} position={grassPosition} scale={2.5} />
  {/await}
{/each}

{#each treePositions as treePosition}
  {#await useGltf("/assets/tree.glb") then tree}
    <T is={tree.scene.clone()} position={treePosition} scale={1.8} />
  {/await}
{/each}
