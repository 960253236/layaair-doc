## Unity插件使用



### 下载LayaAir3D导出工具

下载地址http://ldc.layabox.com/download/tools/LayaAir3DConvertTools.zip

或者在ide下 菜单-----工具----3D转换工具（图1）。

下载完成后我们可以看到两款工具，一款是用于转换FBX格式的FBXTools工具，此工具目前暂时不会再维护更新，建议开发者们使用另一款unity导出插件工具，更方便开发者们搭建游戏世界并导出使用。

![图片1](img/1.png)<br>（图1）



### 安装导出插件

启动unity，新建个项目，并导入游戏需要的资源与材质、贴图等，项目名称可以按照自己的需要来命名。ctrl+s保存我们的场景，我们这里保存名字叫truck。

在资源管理界面右键导入LayaAir3D转换工具。插件版本会随着LayaAir引擎功能的增加而更新，但导入的方法是完全一致的。

导入工具成功后，在资源管理界面中会出现一个名为LayaPlugin文件夹，同时在unity菜单栏中也会出现导出插件菜单LayaPlugin。如图2：

![动图2](img/2.gif)<br>（图2）

​

### 导出资源设置

我们在unity中创建一个汽车模型，然后我们用LayaAir的插件导出。点击菜单栏LayaPlugin，会出现导出设置面板，在这我们将详细为大家讲解。

![动图3](img/3.gif)<br>（图3）



#### 导出资源类别

**Scene类别**是指的整个场景，无论场景中的模型、材质、贴图、动画、还是光照贴图全部导出，主要用于场景制作，文件扩展名是.ls，需要用Scene类或它的继承类加载。

**Sprite3D类别**比场景少了光照贴图的导出，经常用于角色或游戏中活动物品的单独资源导出，文件扩展名的是.lh，要用Spite3D加载。

它们的加载我们将在“3D技术文档—LayaAir3D之模型篇"介绍。

#### Mesh Setting

网格数据的导出设置，勾选后出现两条信息（图4），它们的可起到压缩模型网格lm文件大小的作用，建议如项目中不用切线（不用法线贴图）与顶点色，请都勾选，可节省20%左右的模型资源大小。

Ignore Vertices Tangent       忽略顶点切线信息
Ignore Vertices Color            忽略顶点颜色信息

![图片4](img/4.png)<br>（图4）



#### Texture Setting

贴图导出设置，勾选后出下如（图5）信息，在layaAir引擎中只支持png与jpg格式的图片，如果项目中使用了其它格式，游戏加载时会报错，因此需要转换。

Original Texture Type　需要转换格式的原始纹理格式种类
Non-PNG|JPG　　非png|jpg 现在支持 tga、psd、gif、tif、bmp、exr格式
PNG、JPG　　　　原始场景中所用png格式资源及所用jpg格式资源
LightMap　　　　光照贴图，（只有选择Scene类别导出才会有），建议手动ps处理

Target Texture Type　 转换目标纹理类型
PNG 　　　　　　 转换成png格式，带透明通道
JPG　　　　　　　转换为jpg附带压缩功能，可选择压缩质量

![图片5](img/5.png)<br>（图5）



#### Animation Setting

动画导出设置（图6）

Optimize Bones   删除动画中无用骨骼，只删除不影响骨骼动画播放的无用骨骼，如果需要做骨骼挂点，请谨慎选择
Compress Lsani   暂时无用，开发中，压缩骨骼动画数据，减小文件大小

![图片6](img/6.png)<br>（图6）



#### GameObject Setting 

游戏物品节点设置（图7）

Ignore Null Game Objects 
导出时忽略空节点，LayaAir引擎不支持的节点也记作空节点，如照相机节点，灯光节点，可减少精灵数。

Ignore Not Active Game Objects 
导出时忽略在unity场景中未激活的节点。

Optimize Game Objects 
导出时从unity场景中第一级节点开始拍平树形结构，删除所有无用节点，可最大程度减少精灵数。

Batch Make The First Level Game Objects 
批量导出（必须选择sprite3d才会有）批量导出场景中所有一级节点。

 ![图片7](img/7.png)<br>（图7）




#### Other Setting

其他设置（图8）

Cover Original Export Files 
导出时覆盖原始导出文件

Customize Export Root Directory Name 
自定义导出文件夹名字，默认的文件夹名字为“layaScene+场景名”。

Automatically Save The Configuration 
导出时自动保存当前配置

 ![图片8](img/8.png)<br>（图8）



#### 导出设置

Borower 保存的文件路径
Clear  清空当前配置
Revert 从配置表中读取已保存配置
Save   保存当前配置，保存后，下次打开后会直接使用之前配置，方便开发者们操作。
Laya Export  导出当前资源，点击后，将导出当前场景或模型的数据到指定路径上。

 ![图片9](img/9.png)<br>（图9）





### 导出的资源简单介绍

当配置好输出场景设置后，点击Laya Export 按钮，导出后生成了默认的LayaScene_truck文件夹（图10）。

 ![图片10](img/10.png)<br>（图10）

见上图文件资源，导出后生成了.ls、.lm、.lmat数据资源，及贴图png、tga资源。

.ls为场景文件，选择导出Scene类别时生成，包含了场景需要的各种数据，模型、光照贴图、位置等，需用Scene类加载。

.lh为模型文件，选择导出Sprite3D类别时生成，缺少光照贴图文件信息，其他与.ls相同。

.lm为模型数据文件，相当于FBX格式的转换，可用MeshSprite3D类加载。

.lmat为材质数据文件，是在unity中为模型设置的材质信息，加载.ls或.lh文件时会自动加载.lmat产生材质。.lmat还可手动修改其中某些属性。

.lani为动画数据文件（图10中模型未有动画，因此导出时未生成），如果模型上有动画，导出后将生成动画配置文件，包含了骨骼或帧动画信息。

它们的具体用法，将在后续课程文档中详细介绍。



### 简单加载实例

我们把LayaScene_truck文件夹内容全部复制到项目的根目录的bin/h5/下。

Tips：本章节中只介绍简单加载应用，导出后会生成各种格式，它们的详细说明我们将在3D技术文档中“LayaAir3D之场景Scene”和“LayaAir3D之模型”篇介绍。

加载场景.ls示例代码如下。

```java
package {
	import laya.d3.core.Camera;
	import laya.d3.core.scene.Scene;
	import laya.d3.math.Vector3;
	import laya.display.Stage;
	import laya.utils.Stat;

	public class LayaAir3D {
		
		public function LayaAir3D() {

			//初始化引擎
			Laya3D.init(0, 0,true);
			Laya.stage.scaleMode = Stage.SCALE_FULL;
			Laya.stage.screenMode = Stage.SCREEN_NONE;
			Stat.show();

			//添加3D场景
			var scene:Scene = Scene.load("LayaScene_truck/truck.ls");
			Laya.stage.addChild(scene);
			
			//创建摄像机(横纵比，近距裁剪，远距裁剪)
			var camera:Camera = new Camera( 0, 0.1, 1000);
			//加载到场景
			scene.addChild(camera);
			//移动摄像机位置
			camera.transform.position=new Vector3(-8, 4, 15);
			//旋转摄像机角度
			camera.transform.rotate(new Vector3( -8, -25, 0), true, false);
		}		
	}
}
```

编译运行上述简单代码，我们发现场景加载成功，场景中的模型也显示到了3D视图上（图10）。

 ![图片11](img/11.png)<br>（图11）

