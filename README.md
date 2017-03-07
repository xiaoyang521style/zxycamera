# zxycamera
<p style="color: #ccc; margin-bottom: 30px;">来自于：开发者</p>

<div class="outline">
[takePictureClick](#a1)

[takeVideoClick](#a2)

[takePictureAndVideoClick](#a3)

[compressVideo](#a4)

[captureScreen](#a5)

[getVideoInfo](#a6)

[compressImg](#a7)

[getImageInfo](#a8)
</div>

#**概述**

**zxycamera**

zxycamera 是仿照微信、QQ的照相和录像一体功能。具有前置、后置、设置闪光灯功能，可预览相片和视频。

**zxycamera 模块概述**

本模块封装了相机功能，把照相和录像放在一个界面，通过手势分为单击照相、长按录像，使用非常简单。能够在相册中创建相册，保存相片和视频到相册中。注意相册和录像也保存到了沙盒路径中tmp目录，当应用关闭时相册和录像会被删除。如有需要请开发者自己对文件操作。视频录像为mov格式，模块中包含的视频和相片的压缩和格式处理接口。使用该模块需要把相机、相册、麦克风权限打开。

## [实例widget下载地址](https://codeload.github.com/xiaoyang521style/zxycamera/zip/master)

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

<div id="a4"></div>
#**compressVideo**

视频压缩，格式转换

compressVideo(params},callback(ret, err))

##params

directories：

- 类型：字符串
- 描述：处理视频的绝对路径

format

- 类型：字符串
- 描述：处理后视频的格式

presetName

- 类型：数字类型
- 描述：处理后视频的分辨率，默认值为1
- 取值范围：
* 0（low,低分辨率）
* 1（Medium，中等分辨率）
* 2（Highest，高分辨率）
* 3（640x480 分辨率）
* 4（960x540 分辨率）
* 5（1280x720 分辨率）
* 6（1920x1080 分别率）
* 7（3840x2160 分辨率）

##callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```js
{
    state: 0      //数字类型；0代表视频处理成功，1代表视频处理失败。
    compressPath:""//字符串类型；视频处理后的文件路径
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
var zxycamera = api.require('zxycamera');
zxycamera.compressVideo({
    directories:'',
    format:'mp4',
    presetName:1
},function(ret,err){
    alert(JSON.stringify(ret));
});

```

##可用性

iOS系统

可提供的1.0.0及更高版本

<div id="a5"></div>
#**captureScreen**

截取视频任意时间点静态图

captureScreen({params}, callback(ret, err))

##params

path：

- 类型：字符串
- 描述：处理视频的绝对路径

startTime：

- 类型：数字类型
- 描述：（可选项）截屏时间点，数量级为秒，如0，3.5，10等。
- 默认值：0

##callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```js
{
    state: 0      //数字类型；0代表视频图片截取成功，1代表视频图片截取失败。
    imgPath:''    //字符串类型；视频图片路径
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
var zxycamera = api.require('zxycamera');
zxycamera.captureScreen({
    path:'',
    startTime:0
},function(ret,err){
    alert(JSON.stringify(ret));
});

```

##可用性

iOS系统

可提供的1.0.0及更高版本

<div id="a6"></div>
#**getVideoInfo**

获取视频信息

getVideoInfo({params}, callback(ret, err))

##params

path：

- 类型：字符串
- 描述：处理视频的绝对路径

##callback(ret, err)

ret：

- 类型：JSON 对象
- 内部字段：

```js
{
duration: ''  //字符串类型；视频总时长，以秒为单位
natural:''    //字符串类型；视频分辨率
fileSize:''   //字符串类型；视频大小，单位 byte 
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

var zxycamera = api.require('zxycamera');
zxycamera.getVideoInfo({
    path:''
},function(ret,err){
    alert(JSON.stringify(ret));
});

```

##可用性

iOS系统

可提供的1.0.0及更高版本

<div id="a7"></div>
#**compressImg**

压缩图片

compressImg({params}, callback(ret, err))

##params

path

- 类型：字符串
- 描述：处理图片的绝对路径

compressionQuality

- 类型：字符串
- 描述：压缩图片比例。默认为1，取值在0到1之间。

##callback(ret, err)

ret

- 类型：JSON 对象
- 内部字段：

```js
{
    compressPath:'' //压缩图片存放地址
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

var zxycamera = api.require('zxycamera');
zxycamera.compressImg({
    path:''
    compressionQuality:1
},function(ret,err){
    alert(JSON.stringify(ret));
});

```


##可用性

iOS系统

可提供的1.0.0及更高版本

<div id="a8"></div>
#**getImageInfo**

压缩图片

getImageInfo({params}, callback(ret, err))

##params

path

- 类型：字符串
- 描述：要获取图片信息的绝对地址



ret

- 类型：JSON 对象
- 内部字段：

```js
{
    data:                   //数字类型；视频大小，单位 byte 
    imageNaturalSize:       //字符串类型；图片分辨率
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

var zxycamera = api.require('zxycamera');
zxycamera.getImageInfo({
    path:''
},function(ret,err){
    alert(JSON.stringify(ret));
});

```
##可用性

iOS系统

可提供的1.0.0及更高版本



