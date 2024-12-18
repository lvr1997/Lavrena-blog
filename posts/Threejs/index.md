# Threejs

> Threejs是一个基于JavaScript的3D渲染引擎，用于快速创建三维场景。  --- [threejs官网](https://threejs.org/)

2024年07月：工作上涉及到一些3D场景方面的知识，花了两三天的时间**入门**一下

## 基本概念

### 光源对物体的影响

#### 点光源

```js
//创建点光源
const light = new THREE.PointLight( 0xffffff, 1);
light.position.set(100, 100, 100);
scene.add( light );

// 光源辅助观察
const pointLightHelper = new THREE.PointLightHelper(light, 10);
scene.add(pointLightHelper);
```

## 性能监视

引入性能监视器stats.js监控电脑性能变化

```js
// 测试电脑渲染性能
const geometry = new THREE.BoxGeometry(5, 5, 5);
const material = new THREE.MeshLambertMaterial({
	color: 0x00ffff
});
const num = 1000; //控制长方体模型数量
for (let i = 0; i < num; i++) {
    const mesh = new THREE.Mesh(geometry, material);
    // 随机生成长方体xyz坐标
    const x = (Math.random() - 0.5) * 200
    const y = (Math.random() - 0.5) * 200
    const z = (Math.random() - 0.5) * 200
    mesh.position.set(x, y, z)
    scene.add(mesh); // 模型对象插入场景中
}
```

```js
//引入性能监视器stats.js
import Stats from 'three/addons/libs/stats.module.js';
//创建stats对象
const stats = new Stats();
//stats.domElement:web页面上输出计算结果,一个div元素，
document.body.appendChild(stats.domElement);
```

## 几何体模型顶点Point
> 用于创建自定义模型

BufferGeometry 空的几何体对象
- 通过类型化数组Float32Array创建顶点数据
- BufferAttribute创建属性缓冲对象  3个为一组
- 点模型渲染几何体的顶点数据
- 线模型渲染几何体的顶点数据
- 网格模型渲染几何体的顶点数据

## Group层级模型（树结构）案例

## 纹理贴图和UV坐标
uv坐标作用：将一个图片剪裁后 贴在几何体上

## 大型3D场景搭建

### 存在的问题

1. 性能问题：传统threejs的渲染性能问题，需要将几何体拆分成多个小模型，再组合成一个大的模型。
2. 场景贴图渲染：需要地理信息数据

