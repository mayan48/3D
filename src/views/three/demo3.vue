<template>
    <div id="demo1">

    </div>
</template>

<script lang="ts" setup>
//引入
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js'//相机控件
import {onMounted} from "vue";
import * as THREE from "three";

let scene, camera, mesh, renderer, controls;

onMounted(() => {
    init()
})

const init = () => {
    createScene();
    createMesh();
    createLight();
    createCamera();
    createRender();
    createControls();
    render();


}

//创建场景
const createScene = () => {
    scene = new THREE.Scene()
}

//创建网格模型
const createMesh = () => {
    //创建一个球体几何对象
    const geometry = new THREE.SphereGeometry(100, 25, 25);
    // 创建一个点材质对象
    const  material = new THREE.PointsMaterial({
        color: 0x0000ff, //颜色
        size: 3, //点渲染尺寸
    });
    //点模型对象  参数：几何体  点材质
    const point = new THREE.Points(geometry, material);
    scene.add(point); //网格模型添加到场景中
}
// 创建光源
const createLight = () => {
    const point = new THREE.PointLight(0xffffff);
    point.position.set(400, 200, 300);
    scene.add(point);

    const ambient = new THREE.AmbientLight(0x66666);
    scene.add(ambient)
}
// 创建相机
const createCamera = () => {
    camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(200, 300, 200);
    camera.lookAt(scene.position)
}
// 创建渲染器
const createRender = () => {
    renderer = new THREE.WebGLRenderer();
    renderer.setSize(1100, 550);
    renderer.setClearColor(0x3f3f3f, 1);
    const element = document.getElementById('demo1');
    element.appendChild(renderer.domElement)
}
// 创建控件对象(鼠标控制旋转，移动)
const createControls = () => {
    controls = new OrbitControls(camera, renderer.domElement);
    controls.autoRotate = true;

}
// 7.渲染
const render = () => {
    controls.update();
    renderer.render(scene, camera);
    requestAnimationFrame(render)
}


</script>

<style scoped lang="less">

#demo1 {
    width: 100%;
    height: 100%;
}

</style>