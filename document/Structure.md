# Structure
### 大致GBuffer渲染流程
```mermaid
graph LR
   模型加载/计算细分几何着色器添加成员 --> 非半透明物体渲染到屏幕空间GBuffer -->|参数:世界坐标,法线,光照参数,视点空间Z-Buffer| 整合所有物体渲染到屏幕空间GBuffer

   半透明物体渲染屏幕空间OITBuffer -->|参数:IOTBuffer与OIT链表| 整合为半透明色彩TBuffer -->|参数:TBuffer| 计算屏幕光照
   整合所有物体渲染到屏幕空间GBuffer -->|参数:GBuffer| 计算屏幕光照

   计算屏幕光照 --> 计算屏幕反射
   模型加载/计算细分几何着色器添加成员 --> 半透明物体渲染屏幕空间OITBuffer
```
### 大致模型继承
```mermaid
graph TD
	元物体 --> 平面
	平面 --> 材质平面
	元物体 --> 球
	平面 --> 水平面-半透明
	元物体 --> 网格模型
```
元物体要保证能够分辨不透明pass和透明pass
### 大致光源继承
```mermaid
graph TD
	元光源 --> 平行光源
	元光源 --> 点光源-不一定
```
### 大致纹理继承
```mermaid
graph TD
	元纹理 --> 贴图纹理
	元纹理 --> 程序纹理
```
噪声腐蚀效果