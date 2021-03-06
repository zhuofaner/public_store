# 做视频素材的移动管理应用



##1. 建立统一映射



本地拍摄

手机路径名称：

内部存储/DCIM/Camera/VID_20201221_152351.mp4



网络视频

http:// * /*.mp4



映射成虚拟视频素材名称 

​		-> 果酱V视(播放)

​		-> 导出成为 fcpxml 格式 (时间轴格式)



## 2.素材同源

> 比如来源于同一个素材名称的不同版本:
>
> 分为【时长不同】：
>
> ​	经其他软件变速后、经过剪辑导出后
>
> 和 【时长相同】：
>
> ​	经过调色、配音、添加特效后

同源的视频路径不同，但在素材逻辑上属于同一分类，进行统一管理。



## 3.素材同族

> 如果一个经过处理生成的视频其源视频还是基于另一个源视频处理而来，而这些视频称为同族视频，该族群的最顶层不再具有源视频的视频称为原始视频。



## 4. 类比 Final Cut Pro 和 PS

在FCP中素材管理分为 资源库(文件夹)、事件(子文件夹)、项目(剪辑)、片段(视频)

其中资源库为了方便管理所有资源(实体文件)

事件最为灵活，包含项目和片段，在操作系统中事件和项目是在资源库(MAC结构文件夹)下以单独的子文件夹呈现的，内含fcp二进制文件 fcpevent，而区别在于事件下还有一个单独的结构 - Origin Media、Render Files 和 Transcoded Media，用于存放片段

其中 Origin Media 放的是原始视频的软链接，原始视频移动，改名都会实时检测到并且做到更改，除非原始视频被删除，否则在工程当中的片段都会通过引用到原始视频和正常显示。

其中 Render Files 文件夹放置的是软件实时生成的缓存文件，删除不影响工程

Transcoded Media 放置的是解码后的文件(源文件m4a解码后变成mov)删除后不影响工程，但会降低视频质量

> 注意：Final Cut Pro 中是不能在项目中引用项目的，必须要从项目导出视频后作为新的片段才能被引用

但是PS中是可以在项目中引用其他项目的，以便于一次修改到处更新。

为此【果酱V视】的视频版本可以在两个不同的视频上进行【描述性归类】，将分散在相同手机里的不同时间拍摄的视频，使用不同app导出的视频，存放在不同手机上的视频，以相同项目的组织形式进行【规约】



## 5. 粗剪

建立命名和分类是视频素材排列组合的根基，【规约】之后再对命名素材(版本分支)拖拽到时间轴上进行预览、粗剪和加工。



## 6. 建立字幕

拥有时间轴是建立字幕的根基，否则字幕就仅仅是文字。





















