# zxycamera
<p style="color: #ccc; margin-bottom: 30px;">

<div class="outline">
[takePictureClick](#a1)

[takeVideoClick](#a2)

[takePictureAndVideoClick](#a3)
</div>

#**概述**

**zxycamera**

zxycamera 是仿照微信、QQ的照相和录像一体功能。具有前置、后置、设置闪光灯功能，可预览相片和视频。

**zxycamera 模块概述**

本模块封装了相机功能，把照相和录像放在一个界面，通过手势分为单击照相、长按录像，使用非常简单。能够在相册中创建相册，保存相片和视频到相册中。注意相册和录像也保存到了沙盒路径中tmp目录，当应用关闭时相册和录像会被删除。如有需要请开发者自己对文件操作。视频录像为mov格式，没有进行压缩和格式处理（视频处理videoTool模块正在审核中，即将上架）。使用该模块需要把相机、相册、麦克风权限打开。

## [实例widget下载地址](https://codeload.github.com/xiaoyang521style/ZXYcamera/zip/master)

**模块使用攻略**

##**模块接口**

<div id="a1"></div>
#**takePictureClick**

调用照相功能

takePictureClick({params}, callback(ret, err))

##params

albumName：

- 类型：字符串
- 描述：创建系统相册的名字，建议使用app名字。

##callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```js
{
    image:      //字典类型； 相片返回信息
    {
        imagePath:"",           // 字符串；相片地址 绝对地址
        imageName:"",           // 字符串；相片名字
        imageFormat:"",         // 字符串；相片格式 格式 png
        imageRatio:"",          // 字符串；相片像素 720 x 1280
        imageFileSize:""        // 字符串；相片大小  单位 byte 
    }  
    video：""                //无视频信息返回
}
```

err：

- 类型：JSON 对象
- 内部字段：

```js
{
        //无返回值
}
```


##示例代码

```js
var camera = api.require('zxycamera');
camera.takePictureClick({
    albumName:'UZAPP'
},function(ret,err){
    alert(JSON.stringify(ret));  
});
```
iOS支持版本8.0以上 


<div id="a2"></div>
#**takeVideoClick**

调用录像功能

takeVideoClick({params}, callback(ret, err))

##params

albumName：

- 类型：字符串
- 描述：创建系统相册的名字，建议使用app名字。

voideLength：

- 类型：字符串
- 描述：录制视频最长时间，单位为秒，使用整数。
- 默认值：10
- 取值范围：大于0的数

##callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```js
{
    image:      //字典类型； 视频封面图片返回信息
    {
        imagePath:"",           // 字符串；相片地址 绝对地址
        imageName:"",           // 字符串；相片名字
        imageFormat:"",         // 字符串；相片格式 格式 png
        imageRatio:"",          // 字符串；相片像素 720 x 1280
        imageFileSize:""        // 字符串；相片大小  单位 byte 
    }  
    video:  //字典类型； 视频返回信息
    {
        videoPath:"",           // 字符串；视频地址  绝对地址
        videoName:"",           // 字符串；视频名字
        videoFormat:"",         // 字符串；视频格式  格式mov
        videoRatio:"",          // 字符串；视频像素  720 x 1280
        videoFileSize:"",       // 字符串；视频大小  单位 byte 
        videoDuration:""        // 字符串；视频时长  单位 秒
    }
}
```

err：

- 类型：JSON 对象
- 内部字段：

```js
{
//无返回值
}
```

##示例代码

```js
var camera = api.require('zxycamera');
camera.ttakeVideoClick({
    albumName:'UZAPP'
},function(ret,err){
    alert(JSON.stringify(ret));  
});
```
iOS支持版本8.0以上 

<div id="a3"></div>
#**takePictureAndVideoClick**

调用照相和录像功能

takePictureAndVideoClick({params}, callback(ret, err))

##params

albumName：

- 类型：字符串
- 描述：创建系统相册的名字，建议使用app名字。

voideLength：

- 类型：字符串
- 描述：录制视频最长时间，单位为秒，使用整数。
- 默认值：10
- 取值范围：大于0的数

##callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```js
{
    image:      //字典类型； 相片或视频封面返回信息
        {
            imagePath:"",           // 字符串；相片地址 绝对地址
            imageName:"",           // 字符串；相片名字
            imageFormat:"",         // 字符串；相片格式 格式 png
            imageRatio:"",          // 字符串；相片像素 720 x 1280
            imageFileSize:""        // 字符串；相片大小  单位 byte 
        }  
    video:  //字典类型； 视频返回信息
        {
            videoPath:"",           // 字符串；视频地址  绝对地址
            videoName:"",           // 字符串；视频名字
            videoFormat:"",         // 字符串；视频格式  格式mov
            videoRatio:"",          // 字符串；视频像素  720 x 1280
            videoFileSize:"",       // 字符串；视频大小  单位 byte 
            videoDuration:""        // 字符串；视频时长  单位 秒
        }
}
```
err：

- 类型：JSON 对象
- 内部字段：

```js
{
        //无返回值
}
```

##示例代码

```js
var camera = api.require('zxycamera');
camera.takePictureAndVideoClick ({
    albumName:'UZAPP',
    voideLength:'20'
}, function(ret, err) {
    alert(JSON.stringify(ret));
});

```
##补充说明

当video为""时候是拍照，否则为录制视频。拍照、录制视频image里面都有属性。当为录像时，image为视频封面图片信息。

##可用性

iOS支持版本8.0以上 

