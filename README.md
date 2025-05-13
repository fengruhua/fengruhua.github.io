<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>我的3D自我介绍</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      display: flex;
      height: 100vh;
      font-family: "Segoe UI", sans-serif;
      background-color: #f0f2f5;
      color: #333;
    }
    .info-panel {
      width: 40%;
      padding: 50px;
      background-color: #ffffff;
      box-shadow: 5px 0 15px rgba(0,0,0,0.05);
    }
    .info-panel h1 {
      color: #0077cc;
      margin-bottom: 10px;
    }
    .info-panel p {
      margin: 10px 0;
    }
    .model-viewer {
      width: 60%;
      height: 100%;
    }
    canvas {
      display: block;
      width: 100%;
      height: 100%;
    }
  </style>
</head>
<body>
  <div class="info-panel">
    <h1>你好，我是张三 👋</h1>
    <p>🎓 专业：计算机科学</p>
    <p>💼 职业：三维图形开发者</p>
    <p>🛠️ 技能：WebGL / Three.js / Blender</p>
    <p>📫 邮箱：zhangsan@example.com</p>
    <p>🌐 博客：<a href="https://myblog.com">https://myblog.com</a></p>
    <p>📁 GitHub：<a href="https://github.com/yourusername">yourusername</a></p>
  </div>
  <div class="model-viewer" id="viewer"></div>

  <!-- 引入 Three.js 与 GLTF 加载器 -->
  <script src="https://cdn.jsdelivr.net/npm/three@0.157.0/build/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.157.0/examples/js/loaders/GLTFLoader.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.157.0/examples/js/controls/OrbitControls.js"></script>

  <script>
    const container = document.getElementById('viewer');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(container.clientWidth, container.clientHeight);
    container.appendChild(renderer.domElement);

    const light = new THREE.HemisphereLight(0xffffff, 0x444444);
    light.position.set(0, 20, 0);
    scene.add(light);

    const loader = new THREE.GLTFLoader();
    loader.load('model/your_model.glb', function(gltf) {
      scene.add(gltf.scene);
      gltf.scene.position.set(0, -1, 0);
      gltf.scene.scale.set(1.5, 1.5, 1.5);
      animate();
    }, undefined, function(error) {
      console.error('加载模型出错：', error);
    });

    const controls = new THREE.OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;

    camera.position.set(0, 1.5, 3);
    controls.update();

    function animate() {
      requestAnimationFrame(animate);
      controls.update();
      renderer.render(scene, camera);
    }

    window.addEventListener('resize', () => {
      camera.aspect = container.clientWidth / container.clientHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(container.clientWidth, container.clientHeight);
    });
  </script>
</body>
</html>
