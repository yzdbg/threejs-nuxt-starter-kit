<template>
  <div id="sceneContainer"></div>
</template>

<script>
import * as THREE from 'three';

export default {
  name: 'IndexPage',
  data() {
    return {
      scene: null,
      camera: null,
      renderer: null,
      geometry: null,
      material: null,
      sphere: null,
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      // Initialize the scene
      this.scene = new THREE.Scene();

      // Initialize the camera
      this.camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );
      this.camera.position.z = 60;

      // Initialize the renderer
      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      document
        .getElementById('sceneContainer')
        .appendChild(this.renderer.domElement);

      // Initialize the geometry
      this.geometry = new THREE.SphereGeometry(30, 32, 32);

      // Load the texture
      const textureLoader = new THREE.TextureLoader();
      textureLoader.load('https://i.postimg.cc/L6BTDGy1/taha.png', (texture) => {
        // **Set texture wrapping and repeat**
        texture.wrapS = THREE.RepeatWrapping;
        texture.wrapT = THREE.RepeatWrapping;
        texture.repeat.set(4, 1); // Repeat twice horizontally and vertically

        // Create the material with the texture
        this.material = new THREE.MeshBasicMaterial({
          map: texture,
        });

        // Create the sphere mesh
        this.sphere = new THREE.Mesh(this.geometry, this.material);
        this.scene.add(this.sphere);

        // Start the animation loop
        this.animate();
      });
    },
    animate() {
      requestAnimationFrame(this.animate.bind(this));

      // Rotate the sphere if it's loaded
      if (this.sphere) {
        this.sphere.rotation.y += 0.01;
      }

      // Render the scene
      this.renderer.render(this.scene, this.camera);
    },
  },
};
</script>

<style>
.container {
  margin: 0 !important;
}
body{
  margin: 0;
  overflow: hidden;
}
</style>
