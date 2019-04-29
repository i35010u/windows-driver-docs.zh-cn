---
title: 360 相机视频捕获
description: 提供了有关 360 照相机视频捕获的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8bf634a005b626a64df5a3d394b10bd293199ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357283"
---
# <a name="360-camera-video-capture"></a>360 相机视频捕获

Windows 10 版本 1803年为 360 摄像头预览、 捕获和记录与现有的 MediaCapture Api 提供支持。 这使平台以显示球形帧源 （例如，equirectangular 帧），因而应用程序可以检测和处理 360 视频摄像机流提供 360 捕获体验。

> [!NOTE]
> [Cam360](https://github.com/Microsoft/Windows-Camera/tree/master/Tools/Cam360) GitHub 上提供的示例演示如何使用 Windows 上 360 照相机支持预览、 视频录制和照片捕获方案。

## <a name="overview"></a>概述

360 照相机 IHV 可以提供将公开的每个流的球面格式的 DMFT 插件 （有或没有自定义 UVC 驱动程序） 和媒体类型，会发出球面帧以及过程照相机的驱动程序输出，并提供使用 equirectangular 帧相应的属性和元数据。

大多数 360 相机附带 2 个连续的传感器，覆盖有重叠 360 FoV。 IHV 通常是以同步方式捕获与两个鱼眼传感器，取消变形和拼结在 DMFT 然后输出 equirectangular 帧的帧。

可获取和通过 MediaCapture 和 MediaPlayer Api 投影 360，球形，平移视频预览体验的应用使用的这些 equirectangular 帧。 通过 DMFT 提供的元数据将可供要录制视频 MP4 格式和隐式将适当的标准化元数据的平台。 如播放从内 360 播放视频播放器**电视和电影**上记录的 Windows 10，生成视频应用程序将提供预期的球面视图平移体验。

360 照相机使用情况：

-   用于预览 360 框架，应用程序不必显式使用 XAML [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement)预览版。 此外需要显式处理平移，UI 交互的应用程序通过[MediaPlaybackSphericalVideoProjetion.ViewOrientation](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksphericalvideoprojection)四元数。

-   360 视频记录捕获应用程序不需要如果它使用的，显式配置 360 内容[MediaCapture WinRT Api](https://docs.microsoft.com/windows/uwp/audio-video-camera/basic-photo-video-and-audio-capture-with-mediacapture)，如球面格式是隐式传递到记录接收器和写入文件标头。

-   360 照片捕获时，应用程序需要显式添加相应的标准化元数据，指定使用可用其球面格式[WIC WinRT Api](https://docs.microsoft.com/windows/uwp/audio-video-camera/image-metadata)。

负责 360 照相机 IHV 能够实现预计视图的流，并公开扫视/倾斜/缩放控件。

应用程序可能会实现并插入要生成投影效果。 效果可以利用 mediatype 来标识 equirectangular 帧上的属性。


## <a name="architecture"></a>体系结构


下图说明了到 360 照相机堆栈 DMFT 的关系：

![360 照相机堆栈](images/360-camera-stack.png)

360 照相机 Ihv 将发布 DMFT 将公开提供的定义的格式的球面帧 360 视频流。 可以安装并与通过驱动程序扩展该示例中所述的 INF 文件使用特定的相机关联 DMFT。下面的 INF。

拼接和转换为 equirectangular 帧可以发生在照相机硬件或 DMFT 内。 它可能会更可取的方法实现此目的，利用 DMFT，因为它允许针对高效处理等 GPU 硬件资源的使用。 DMFT 还将填充以下流和媒体类型属性 （如在下表中所示） 以标识为 360 内容流。

即使 IHV 决定有摄像机硬件中完成 stiching，DMFT 仍是必需的要求来填充流和媒体类型 360 视频的特性属性。

下表显示了所需的流属性来标识球面帧源：

<table>
<thead>
<tr class="header">
<th>属性名称和 GUID</th>
<th>
<p>值</p>
</th>
<th>
<p>特性</p>
</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="_Hlk495398335" class="anchor"><span id="_Hlk495398374" class="anchor"></span></span>MF_SD_VIDEO_SPHERICAL<br />
{A51DA449-3FDC-478C-BCB5-30BE76595F55}</td>
<td>
<p>TRUE (1)</p>
</td>
<td>
<p>Stream 和媒体类型</p>
</td>
</tr>
<tr class="even">
<td><span id="_Hlk495398361" class="anchor"><span id="_Hlk495398391" class="anchor"></span></span>MF_SD_VIDEO_SPHERICAL_FORMAT<br />
{4A8FC407-6EA1-46C8-B567-6971D4A139C3}</td>
<td>
<p>MFVideoSphericalFormat_Equirectangular (1)</p>
</td>
<td>
<p>MediaType</p>
</td>
</tr>
</tbody>
</table>

上述属性已存在的一部分**mfidl.idl**。

若要利用自定义应用的执行以及拼接，IHV 必须具有属性设置为 MF 公开另一种 unstitched 360 视频媒体类型的选项\_SD\_视频\_球面\_格式为MFVideoSphericalFormat\_Unsupported(0)。 自定义应用程序将必须选择未处理的流，并对其进行处理。

## <a name="platform-guidance"></a>平台指南

该平台已公开给应用程序中通过 WinRT 图层的所有流属性[MediaFrameSourceInfo.Properties](https://docs.microsoft.com/uwp/api/windows.media.capture.frames.mediaframesourceinfo)，这可以在其中搜索 MF\_SD\_视频\_球面在上表中定义的 GUID。 但是，大多数平台元素的球面配置将隐式管理平台。 可以通过仅对任何应用程序开发人员可能想要实现，例如，先插入或删除具体取决于视频的 sphericalness 任何自定义效果的额外功能的应用程序查询属性。

平台会绕过人脸检测、 场景分析器和视频防抖动的收件箱效果 （如果添加） 检测到流特性属性值，该值指示球面帧源时。

在平台隐式配置连接以获取预览版 360 视频投影体验的媒体播放器元素。 该应用程序来调用相应的平台 Api，以选择预览版为媒体播放器元素。 应用程序还必须实现用户界面来控制媒体播放器的投影方向和角度。 如果应用程序选择捕获元素为预览版，不能利用球面投影体验。

平台还将隐式配置 MP4 接收器 360 视频录制 （传递相应的视频球面格式和相关元数据如果有提供和支持） 时使用的流包含表 1 – 中定义的属性需要为流属性识别球面帧源。

| **MF\_SD\_视频\_球面\_格式值 (MFVideoSphericalFormat)**  | **SphericalVideoFrameFormat 值** | **解释**  |
|---|---|---|
| 在媒体类型属性中找到的属性设置为值 MFVideoSphericalFormat\_Equirectangular (1) | SphericalVideoFrameFormat。 Equirectangular | 流提供 equirectangular 格式通过 MediaPlayer 元素，可查看球面帧。 |
| 在媒体类型属性中找到的属性设置为值 MFVideoSphericalFormat\_不受支持 (0)     | SphericalVideoFrameFormat。 不支持     | 流提供了另一种格式不兼容与 MediaPlayer 元素的球面帧。 （可能自定义格式支持的某些应用程序） |
| 属性不存在从媒体类型属性。                                                   | SphericalVideoFrameFormat。 无            | 流提供普通非球面框架。 (非 360) |

## <a name="application-guidance"></a>应用程序指南

应用程序可以使用[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) XAML 控件，以充分利用 360 视频球面投影经验。

如果 MF\_SD\_视频\_球面\_格式属性上的媒体类型存在并且设置为 MFVideoSphericalFormat\_Equirectangular，帧然后应为球形，可以是通过适当地呈现[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) XAML 控件。 应用程序可以查询球面 media player 检测到通过检查 MediaPlaybackSphericalVideoProjection 从媒体播放器播放会话 (objMediaPlayer.PlaybackSession.SphericalVideoProjection) 获取属性的格式。 应用程序必须设置**isEnabled**属性设置为**TRUE**启动球面的投影。

如果应用程序实现其自己的自定义球面的投影组件，则它可以查询框架源通过其[MediaFrameSourceInfo.Properties](https://docs.microsoft.com/uwp/api/windows.media.capture.frames.mediaframesourceinfo)球面流级别视频属性表中所述上面。 但是，所有平台元素配置 media player 预览版和等平台上检测到的流和 mediatype attribuites 上的照相机 DMFT 公开的球面视频属性将隐式配置记录的接收器。



## <a name="inf-file-example-to-publish-a-dmft"></a>.若要发布 DMFT 的 INF 文件示例

```INF
;=================================================================================
; Microsoft Sample Extension INF for USB Camera SampleDeviceMFT installation
; Copyright (C) Microsoft Corporation. All rights reserved.
;=================================================================================

[Version]
Signature="$WINDOWS NT$"
Class=Extension
ClassGUID={e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider=%CONTOSO%
ExtensionId = {E4FE3A00-68CF-45A3-83C8-8347A6A38069} ; replace with your own GUID
CatalogFile.NT = SampleExtensionInfForDmftInstallation.cat
DriverVer=08/28/2017,10.0.17000.2000

[Manufacturer]
%CONTOSO% = ContosoSampleDeviceMFT,ntamd64

[ContosoSampleDeviceMFT.ntamd64]
%ContosoCamera.DeviceDesc% = ContosoSampleDeviceMFT_Install, usb\vid_xxxx&pid_xxxx&mi_xx  ; replace with your camera device VID PID

[ContosoSampleDeviceMFT_Install]
CopyFiles=ContosoSampleDeviceMFTCopy
AddReg=ContosoSampleDeviceMFT_COM.AddReg

;-----------------------------------------------------------------------------------
;
; Registers Device MFT COM object
;
;-----------------------------------------------------------------------------------

[ContosoSampleDeviceMFT_COM.AddReg]
HKCR,CLSID\%SampleDeviceMFT.CLSID%,,,%SampleDeviceMFT.FriendlyName%
HKCR,CLSID\%SampleDeviceMFT.CLSID%InProcServer32\,,,%%SystemRoot%%\ContosoSampleDeviceMFT.dll
HKCR,CLSID\%SampleDeviceMFT.CLSID%InProcServer32\,ThreadingModel,,"Both"

[ContosoSampleDeviceMFT_Install.Interfaces]
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,,ContosoSampleDeviceMFT.Interfaces,

[ContosoSampleDeviceMFT.Interfaces]
AddReg=ContosoSampleDeviceMFT.AddReg

;-----------------------------------------------------------------------------------
;
; Add DeviceMFT CLSID to device interface instance registry key
;
;-----------------------------------------------------------------------------------

[ContosoSampleDeviceMFT.AddReg]
HKR,,CameraDeviceMftClsid,,%SampleDeviceMFT.CLSID%

;-----------------------------------------------------------------------------------
;
; File copy sections
;
;-----------------------------------------------------------------------------------

[SourceDisksFiles]
ContosoSampleDeviceMFT.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[DestinationDirs]
ContosoSampleDeviceMFTCopy=11
DefaultDestDir = 11

[ContosoSampleDeviceMFTCopy]
ContosoSampleDeviceMFT.dll

[Strings]
CONTOSO = "Contoso Inc."
ContosoCamera.DeviceDesc = "Contoso Camera Extension"
MediaDescription="Contoso Camera Sample Device MFT Installation Media"
SampleDeviceMFT.CLSID = "{zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz}" ; replace with your Device MFT COM object's CoClass ID
SampleDeviceMFT.FriendlyName = "Contoso Camera Device MFT"
KSCATEGORY_VIDEO_CAMERA="{E5323777-F976-4f5b-9B55-B94699C46E44}"
```

## <a name="example-frame-flow-with-a-uvc-device"></a>将帧流示例与 UVC 设备

(1) Unstitched 合并来自 USBVdeo.sys 帧：

![Unstitched 组合的帧](images/unstitched-combined.png)

（2） 帧尚未扭曲、 拼接和转换为内发送到应用程序的呈现元素对于预览版，到要存储的视频接收器或照片接收器 DMFT equirectangular 文件：

![帧尚未扭曲、 拼接和转换](images/unwarped-stitched-transformed.png)

（在应用程序使用应用的球面投影，以及提供视区旋转平移和视角交互的用户界面元素 3） 呈现视区：

![呈现的视区](images/rendered-viewport.png)


