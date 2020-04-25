# PictureSelector 2.0
   A Picture Picker For Android Platform, Support From the album to obtain pictures, video, audio & photo, support clipping (single picture or multi-picture clipping), compression, theme custom configuration and other functions, support dynamic access & adapt to Android 5.0+ system of open source picture selection framework。<br>


[![](https://jitpack.io/v/LuckSiege/PictureSelector.svg)](https://jitpack.io/#LuckSiege/PictureSelector)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg)](https://github.com/LuckSiege)
[![CSDN](https://img.shields.io/twitter/url/http/blog.csdn.net/luck_mw.svg?style=social)](http://blog.csdn.net/luck_mw)
[![I](https://img.shields.io/github/issues/LuckSiege/PictureSelector.svg)](https://github.com/LuckSiege/PictureSelector/issues)
[![Star](https://img.shields.io/github/stars/LuckSiege/PictureSelector.svg)](https://github.com/LuckSiege/PictureSelector)

## Directory
-[Need to know before use](https://github.com/LuckSiege/PictureSelector/wiki/%E7%94%A8%E5%89%8D%E9%9C%80%E7%9F%A5)<br>
-[How to ask Issues?](https://github.com/LuckSiege/PictureSelector/wiki/%E5%A6%82%E4%BD%95%E6%8F%90Issues%3F)<br>
-[Functional features](https://github.com/LuckSiege/PictureSelector/wiki/%E5%8A%9F%E8%83%BD%E7%89%B9%E7%82%B9)<br>
-[The latest version v2.5.3](#The latest version)<br>
-[Update log](https://github.com/LuckSiege/PictureSelector/releases/tag/v2.5.3)<br>
-[The topic configuration-Xml](https://github.com/LuckSiege/PictureSelector/wiki/%E8%87%AA%E5%AE%9A%E4%B9%89%E4%B8%BB%E9%A2%98-Xml%E6%96%B9%E5%BC%8F)<br>
-[The topic configuration-Code](https://github.com/LuckSiege/PictureSelector/wiki/%E8%87%AA%E5%AE%9A%E4%B9%89%E5%8A%A8%E6%80%81%E4%B8%BB%E9%A2%98(%E5%8C%85%E5%90%AB%E8%A3%81%E5%89%AA%E3%80%81%E7%9B%B8%E5%86%8C%E5%90%AF%E5%8A%A8%E5%8A%A8%E7%94%BB)-Code%E6%96%B9%E5%BC%8F)<br>
-[Effect](#Effect)<br>
-[Method of use](https://github.com/LuckSiege/PictureSelector/wiki/%E9%9B%86%E6%88%90%E6%96%B9%E5%BC%8F)<br>
-[Api explain](https://github.com/LuckSiege/PictureSelector/wiki/PictureSelector-Api%E8%AF%B4%E6%98%8E)<br>
-[Open the photo album](#Open the photo album)<br>
-[Open the camera](#Open the camera)<br>
-[Results the callback](https://github.com/LuckSiege/PictureSelector/wiki/%E7%BB%93%E6%9E%9C%E5%9B%9E%E8%B0%83)<br>
-[Common mistakes](https://github.com/LuckSiege/PictureSelector/wiki/%E5%B8%B8%E8%A7%81%E9%94%99%E8%AF%AF)<br>
-[Cache to clear](#Cache to clear)<br>
-[Confusion](#Confusion)<br>
-[LICENSE](#LICENSE)<br>
-[Contact](#Contact)<br>


## The latest version
```sh
implementation 'com.github.LuckSiege.PictureSelector:picture_library:v2.5.3'
```

## Open the photo album
Quick call, more functions [More](https://github.com/LuckSiege/PictureSelector/wiki/PictureSelector-%E5%8A%9F%E8%83%BD%E9%85%8D%E5%88%B6%E9%A1%B9)

onActivityResult
```sh 
 PictureSelector.create(this)
   .openGallery(PictureMimeType.ofImage())
   .loadImageEngine(GlideEngine.createGlideEngine()) // Please refer to the Demo GlideEngine.java
   .forResult(PictureConfig.CHOOSE_REQUEST);
   
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (resultCode == RESULT_OK) {
            switch (requestCode) {
                case PictureConfig.CHOOSE_REQUEST:
                    // onResult Callback
                    List<LocalMedia> selectList = PictureSelector.obtainMultipleResult(data);
                    break;
                default:
                    break;
            }            
        }
```

Callback
```sh
 PictureSelector.create(this)
   .openGallery(PictureMimeType.ofAll())
   .loadImageEngine(GlideEngine.createGlideEngine())
   .forResult(new OnResultCallbackListener<LocalMedia>() {
       @Override
       public void onResult(List<LocalMedia> result) {

         }

       @Override
       public void onCancel() {

         }
      });  
```

## Open the camera
Quick Use, separately start the photo or video according to PictureMimeType automatic recognition [More](https://github.com/LuckSiege/PictureSelector/wiki/PictureSelector-%E5%8A%9F%E8%83%BD%E9%85%8D%E5%88%B6%E9%A1%B9)

onActivityResult
```sh
 PictureSelector.create(this)
   .openCamera(PictureMimeType.ofImage())
   .loadImageEngine(GlideEngine.createGlideEngine()) // Please refer to the Demo GlideEngine.java
   .forResult(PictureConfig.REQUEST_CAMERA);  
   
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (resultCode == RESULT_OK) {
            switch (requestCode) {
                case PictureConfig.REQUEST_CAMERA:
                    // onResult Callback
                    List<LocalMedia> selectList = PictureSelector.obtainMultipleResult(data);
                    break;
                default:
                    break;
            }            
        }
```

Callback
```sh
PictureSelector.create(this)
   .openGallery(PictureMimeType.ofAll())
   .loadImageEngine(GlideEngine.createGlideEngine())
   .forResult(new OnResultCallbackListener<LocalMedia>() {
       @Override
       public void onResult(List<LocalMedia> result) {

         }

       @Override
       public void onCancel() {

         }
      });
```

## Cache to clear
```sh
 // Include clipped and compressed cache, to be called upon successful upload, type refers to the image or video cache depending on which ofImage or ofVideo you set up note: system sd card permissions are required
 PictureFileUtils.deleteCacheDirFile(this,type);
 // Clear all temporary files generated by caching such as compression, clipping, video, and audio
 PictureFileUtils.deleteAllCacheDirFile(this);
```
 
## Preview Image
```
// Preview picture can be customized length press save path
*Prompt .themeStyle(R.style.theme)；Inside the parameters can not be deleted, otherwise crash...

PictureSelector.create(this)
 .themeStyle(R.style.picture_default_style)
 .isNotPreviewDownload(true)
 .loadImageEngine(GlideEngine.createGlideEngine())
 .openExternalPreview(position, selectList);

```
## Preview Video
```sh
PictureSelector.create(this).externalPictureVideo(video_path);
```

## Project USES third-party libraries：

* PhotoView
* luban
* ucrop

## Confusion
```sh
#PictureSelector 2.0
-keep class com.luck.picture.lib.** { *; }

#Ucrop
-dontwarn com.yalantis.ucrop**
-keep class com.yalantis.ucrop** { *; }
-keep interface com.yalantis.ucrop** { *; }

#Okio
-dontwarn org.codehaus.mojo.animal_sniffer.*
```
## LICENSE
```sh
   Copyright 2017 Luck

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```

## Contact
Android Group 1 [619458861]() (biggest) <br>
Android Group 2 [679824206]() (biggest) <br>
Android Group 3 [854136996]() (biggest) <br>
QQ [893855882]() <br>


## Effect

| Single Mode | Mixed Mode |
|:-----------:|:-----------:|
|![](image/home.jpg)|![](image/home_mixed.jpg)| 

| Default Style | Preview | Multiple Crop |
|:-----------:|:--------:|:---------:|
|![](image/picture_default_style_1.jpg) | <img src="image/picture_default_style_2.jpg"/> | ![](image/picture_default_style_new_3.jpg)|  

| Digital Style | Preview | Multiple Crop |
|:-----------:|:--------:|:---------:|
|![](image/picture_num_style_new_1.jpg) | ![](image/picture_num_style_new_2.jpg) | ![](image/picture_num_style_new_3.jpg)| 

| White Style | Preview | Single Crop |
|:-----------:|:--------:|:---------:|
|![](image/picture_sina_style_1.jpg) | ![](image/picture_sina_style_new_2.jpg) | ![](image/picture_sina_style_new_3.jpg)| 

| New Style | Preview | Multiple Crop |
|:-----------:|:--------:|:---------:|
|![](image/picture_wechat_style_1.jpg) | ![](image/picture_wechat_style_2.jpg) | ![](image/picture_wechat_style_new_3.jpg)| 

| Photo Album Directory | Single Mode | Circular Crop|
|:-----------:|:--------:|:--------:|
|![](image/picture_wechat_album_style.jpg) |![](image/picture_wechat_single_style_3.jpg) | ![](image/picture_circular_crop_new_style.jpg)| 

| White Style | Video | Audio |
|:-----------:|:-----------:|:--------:|
|![](image/picture_white_style.jpeg) |![](image/picture_video.jpg) | ![](image/picture_audio.jpg)| 
