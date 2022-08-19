<template>
  <div id="sceneContainer"></div>
</template>

<script>
import * as THREE from 'three';

export default {
  name: 'IndexPage',
    head: {
    bodyAttrs: {
      class: 'container'
    }
  },
  data() {
    return {
      scene: new THREE.Scene(),
      camera: new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000),
      renderer: new THREE.WebGLRenderer(),
      geometry: new THREE.SphereGeometry(15, 24, 16),
      material: new THREE.MeshBasicMaterial({
        color: 0x00ff00,
        wireframe: true
      }),
      cube: null,
    }
  },
  mounted() {
    this.init()
    this.animate()
  },
  methods: {
    init() {
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      const sceneContainer = document.getElementById("sceneContainer")
      sceneContainer.appendChild(this.renderer.domElement);
      this.cube = new THREE.Mesh(this.geometry, this.material)
      this.scene.add(this.cube);
      this.camera.position.z = 60;
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.cube.rotation.y += 0.003
      this.renderer.render(this.scene, this.camera);
    }
  }
}
</script>
<style>
.container{
  margin: 0!important;
}
</style>