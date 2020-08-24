---
title: Three.js 入门
date: 2020-08-24 16:21:00
tags: three.js threejs three
categories: 'JS'
---

### 安装three.js
使用npm安装three.js
```
npm i three -S
```
导入场景、相机、灯光、渲染器等类
```javascript
import { Scene, PerspectiveCamera, WebGLRenderer ,AmbientLight ,DirectionalLight} from "three"
```
创建并暴露一个类，定义场景、相机、灯光等，并设置渲染的DOM容器

<!--more-->
```js
export class Three {
    private scene: Scene
    private camera: PerspectiveCamera
    private renderer: WebGLRenderer
    private $window: HTMLElement
    constructor() {
        this.$window = document.querySelector("#app");
    }
}
```
### 创建场景
初始化一个场景,这里我设置了一个私有方法，之后会在constructor中调用
scene.position.set可以设置场景在坐标系的位置
```js
//创建场景
private initScene(): void {
    this.scene = new Scene();
    this.scene.position.set(0, 0, 0);
    this.scene.lookAt(this.scene.position);
}
```
### 创建相机
接着初始化相机,这里使用的是透视相机PerspectiveCamera，相机接受4个参数，分别是
- PerspectiveCamera(fov, aspect, near, far)
-  Fov – 相机的视锥体的垂直视野角
- Aspect – 相机视锥体的长宽比
- Near – 相机视锥体的近平面
- Far – 相机视锥体的远平面
相机的位置可以使用camera.position.x，camera.position.y，camera.position.z进行赋值来改变
```js
//创建相机
private initCamera(): void {
    this.camera = new PerspectiveCamera(
        25,
        this.$window.clientWidth / this.$window.clientHeight,
        0.1,
        1000
    );
    this.camera.lookAt(0, 0, 0);
}
```
### 创建光源
接着初始化灯光,这里添加了两个灯光，一个环境光，一个平行光，可添加多个光源
灯光的构造函数中传入灯光颜色和透明度，颜色必须是0x+16进制色
环境光没有位置属性，平行光可以添加光源的位置，使用light.position.set来设置位置，传入三个参数分别是x坐标，y坐标，z坐标
```js
//创建光源
private initLight(): void {
    // 环境光
    this.scene.add(new AmbientLight(0xd29c96, 1));
    // 平行光
    let light = new DirectionalLight(0xffffff, 0.6);
    light.position.set(0, 10, 5);
    this.scene.add(light);
}
```
### 创建3D渲染器
接着创建渲染器,使用three内置的WebGLRenderer渲染器来渲染，渲染器可以通过setSize方法设置大小，这里我们设置一个和画布一样大的渲染器，如果渲染尺寸小于画布大小，则超出渲染器大小的位置将不被渲染
使用setClearColor方法可以设置渲染区域的背景色
最后将渲染器的domElement属性appendChild进需要的DOM标签内即可
```js
//创建3D渲染器
private initThree(): void {
    this.renderer = new WebGLRenderer();
    this.renderer.setSize(
        this.$window.clientWidth,
        this.$window.clientHeight
    );
    this.renderer.setClearColor(0xb34149, 1); //设置背景颜色
    this.$window.appendChild(this.renderer.domElement);
}
```
接着将这些方法添加进constructor内，让实例创建时自动执行
```js
export class Three {
    private scene: Scene
    private camera: PerspectiveCamera
    private renderer: WebGLRenderer
    private $window: HTMLElement
    constructor() {
        this.$window = document.querySelector("#app");        
        this.initScene();
        this.initThree();
        this.initCamera();
    }
}
```
### 开启控制器
接着使用renderer.render方法就可以渲染了，但是这样只能渲染一帧画面，我们需要做鼠标控制，或者3D动画是需要实时渲染的
例如加一个鼠标控制
首先导入控制器
```js
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
```
接着初始化这个控制器，这里依然使用一个方法,然后添加进constructor
```js
// 开启控制器
private initControls(): void {
    this.controls = new OrbitControls(this.camera, this.renderer.domElement);
    this.controls.enableDamping = true; // 惯性滑动，滑动大小默认0.25
    this.controls.dampingFactor = 0.05;

    // //控制
    this.controls.enableZoom = false; // 缩放
    this.controls.enableKeys = false; // 键盘
    this.controls.enablePan = false; // 是否开启右键拖拽

    // 旋转速度
    this.controls.rotateSpeed = 1;

    // 自动旋转
    this.controls.autoRotate = false;
    this.controls.autoRotateSpeed = -0.01;

    //设置仰视角和俯视角,后续进行重置
    this.controls.maxPolarAngle = Math.PI / 2;
    this.controls.minPolarAngle = Math.PI / 4;
    this.controls.zoomSpeed = 1;
    //设置相机距离原点的最远距离
    // controls.minDistance = 120;
    //设置相机距离原点的最远距离
    // controls.maxDistance = 120 + 120 * 0.5;
}
```
### 渲染
这样添加的控制器虽然可以控制场景，但是画布不会重新渲染，所以我们需要添加一个渲染函数并且每次调用自身来更新画面
这里使用的是requestAnimationFrame函数来调用自身，也可以使用setInterval但是setInterval是固定时间渲染，如果场景过大，过复杂，可能时间到了还没渲染好又得渲染下一帧，这样会导致页面卡死
requestAnimationFrame没有固定时间，他会在当前帧渲染完毕后执行下一次，这样就不会导致页面卡死了
接着在render方法中使用controls.update()来更新每次的控制，使用renderer.render来更新画面
最后在constructor函数中调用render即可
```js
    private render(): void {
        window.requestAnimationFrame(() => this.render());
        this.controls.update();
        this.renderer.render(this.scene, this.camera);
    }
```
最后在需要需要的地方导入并new Three()就可以了

### 效果
<iframe src="{% asset_path three.html %}" width="600" height="600" frameborder="no" border="0" marginwidth="0" marginheight="0" allowtransparency="yes"></iframe>