---
title: 360 相机视频捕获
description: 提供有关360照相机视频捕获的信息。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f67eddaf082e128f28cdc548c02c9caf20a5478c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184642"
---
# <a name="360-camera-video-capture"></a>360 相机视频捕获

Windows 10 版本1803支持对现有的 MediaCapture Api 进行360相机预览、捕获和记录。 这样一来，平台就可以公开球状帧源 (例如 equirectangular 帧) ，使应用能够检测和处理360视频摄像机流以及提供360的捕获体验。

> [!NOTE]
> GitHub 上提供的 [Cam360](https://github.com/Microsoft/Windows-Camera/tree/master/Tools/Cam360) 示例演示了如何在 Windows 上使用360照相机支持预览、视频记录和照片捕获方案。

## <a name="overview"></a>概述

360相机 IHV 可以提供 (有或没有自定义 UVC 驱动程序的 DMFT 插件) 这将公开发出球状帧的每个流和媒体类型的球面格式，并处理照相机驱动程序输出，并使用相应的属性和元数据提供 equirectangular 帧。

大多数360照相机都提供两个传感器，并覆盖 360 FoV，但有一些重叠。 IHV 通常会与两个 fisheye 传感器同步捕获，unwarp 并将 DMFT 中的帧拼接到，然后输出 equirectangular 帧。

然后，应用可通过 MediaCapture 和 MediaPlayer Api 获取并使用这些 equirectangular 帧，以投影360、球状、平移视频预览体验。 平台将利用通过 DMFT 提供的元数据来记录以 "" 格式提供的视频，并隐式地包含正确的标准化元数据。 从360播放视频播放机（例如 Windows 10 上的 **电影 & 电视** 应用）播放时，所生成的录制视频将提供预期的球状视图平移体验。

360照相机使用：

-   对于预览360帧，应用程序需要显式使用 XAML [MediaPlayerElement](/uwp/api/windows.ui.xaml.controls.mediaplayerelement) for preview。 应用程序还需要显式处理 UI 交互，以通过 [MediaPlaybackSphericalVideoProjetion ViewOrientation](/uwp/api/windows.media.playback.mediaplaybacksphericalvideoprojection) 四元数进行平移。

-   对于360视频记录，如果捕获应用程序使用 [MediaCapture WinRT api](/windows/uwp/audio-video-camera/basic-photo-video-and-audio-capture-with-mediacapture)，则不需要为360内容显式配置该应用程序，因为球状格式将被隐式传递到记录接收器并写入到文件头。

-   对于360照片捕获，应用程序需要使用可用的 [WIC WinRT api](/windows/uwp/audio-video-camera/image-metadata)显式添加适当的标准化元数据，以指定其球状格式。

360相机 IHV 使用投影视图实现流，并公开平移/倾斜/缩放控件。

应用程序可以实现并插入效果以生成投影。 此效果可以利用媒体媒体上的属性来标识 equirectangular 帧。


## <a name="architecture"></a>体系结构


下图说明了 DMFT 与360相机堆栈之间的关系：

![360相机堆栈](images/360-camera-stack.png)

360相机 Ihv 将发布 DMFT，它将公开提供定义格式的球状帧的360视频流。 通过使用用于驱动程序扩展的 INF 文件（如示例中所述），可以安装 DMFT 并将其与特定相机相关联。INF。

在相机硬件或 DMFT 内进行 equirectangular 帧的装订和转换。 最好出于此目的使用 DMFT，因为它将允许使用 GPU 等硬件资源来高效处理。 DMFT 还将填充以下流和媒体类型属性 (如下表中所示) ，以将它们标识为360内容流。

即使 IHV 决定在照相机硬件中完成 stiching，但 DMFT 仍需要填充流和360视频的媒体类型属性属性。

下表显示了用于标识球状帧源的所需流属性：

<table>
<thead>
<tr class="header">
<th>属性名称和 GUID</th>
<th>
<p>Value</p>
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
<p>TRUE (1) </p>
</td>
<td>
<p>流和媒体媒体</p>
</td>
</tr>
<tr class="even">
<td><span id="_Hlk495398361" class="anchor"><span id="_Hlk495398391" class="anchor"></span></span>MF_SD_VIDEO_SPHERICAL_FORMAT<br />
{4A8FC407-6EA1-46C8-B567-6971D4A139C3}</td>
<td>
<p>MFVideoSphericalFormat_Equirectangular (1) </p>
</td>
<td>
<p>MediaType</p>
</td>
</tr>
</tbody>
</table>

上面的属性已作为 **mfidl**的一部分存在。

若要利用执行拼接的自定义应用程序，IHV 可以选择公开其他 unstitched 360 视频媒体类型，并将属性设置为 MF SD 视频球状格式，将其属性设置为 \_ \_ \_ \_ \_ 不支持的 MFVideoSphericalFormat (0) 。 自定义应用程序需要选择未处理的流并对其进行处理。

## <a name="platform-guidance"></a>平台指南

该平台已通过 [MediaFrameSourceInfo](/uwp/api/windows.media.capture.frames.mediaframesourceinfo)为应用程序公开了 WinRT 层的所有流属性，可以搜索 \_ \_ \_ 上表中定义的 MF SD 视频球状 GUID。 不过，平台元素的大多数球面配置将由平台隐式管理。 只有应用程序开发人员可能要实现的任何额外功能（例如，任何需要插入或删除的自定义效果，具体取决于视频的 sphericalness），应用程序才可以查询这些属性。

平台会绕过收件箱效果，如人脸检测、场景分析器和视频稳定 (如果在检测到用于指示球状帧源的流属性属性值时添加) 。

平台为360视频投影体验隐式配置连接到预览版的 media player 元素。 应用程序必须调用适当的平台 Api，才能选择 media player 元素进行预览。 应用程序还必须实现 UI，以控制 media player 的投影方向和角度。 如果应用程序选择用于预览的捕获元素，则不能利用球面投影体验。

当使用的流包含表1中定义的属性时，该平台还会隐式配置 atribute 的接收器来记录 360 (视频，并使用相应的视频球状格式和相关的元) 数据：识别。

| **MF \_ SD \_ 视频 \_ 球状 \_ 格式值 (MFVideoSphericalFormat) **  | **SphericalVideoFrameFormat 值** | **解释**  |
|---|---|---|
| 在 media type 特性中找到的属性设置为 value MFVideoSphericalFormat \_ Equirectangular (1)  | SphericalVideoFrameFormat. Equirectangular | 流提供了 equirectangular 格式的球状帧，可通过 MediaPlayer 元素查看。 |
| 在 media type 特性中找到的属性设置为值 MFVideoSphericalFormat \_ 不支持 (0)      | SphericalVideoFrameFormat. 不支持     | 流提供了另一种格式的球状帧，该格式与 MediaPlayer 元素不兼容。  (可能是某些应用支持的自定义格式)  |
| 属性不存在于 media type 特性中。                                                   | SphericalVideoFrameFormat. 无            | 流提供常规的非球状帧。  (非 360)  |

## <a name="application-guidance"></a>应用程序指南

应用程序可以使用 [MediaPlayerElement](/uwp/api/windows.ui.xaml.controls.mediaplayerelement) XAML 控件来利用360视频球状投影体验。

如果 \_ \_ \_ \_ 媒体类型上存在 MF SD 视频球状 FORMAT 属性，并将其设置为 MFVideoSphericalFormat \_ Equirectangular，则帧将被显示为球面，并可通过 [MediaPlayerElement](/uwp/api/windows.ui.xaml.controls.mediaplayerelement) XAML 控件正确呈现。 应用程序可以通过检查媒体播放器检测到的 MediaPlaybackSphericalVideoProjection 的属性来查询 media player 检测到的球面格式， (objMediaPlayer) 。 应用程序必须将 **isEnabled** 属性设置为 **TRUE** ，才能启动球面投影。

如果应用程序实现其自己的自定义球状投影组件，则它可以通过其 [MediaFrameSourceInfo](/uwp/api/windows.media.capture.frames.mediaframesourceinfo) 来查询帧源，如上表中所述。 不过，平台上的所有平台元素配置（例如 media player preview 和记录接收器）都是在检测到由 DMFT on stream 和媒体媒体 attribuites 公开的球状视频属性时隐式配置的。



## <a name="inf-file-example-to-publish-a-dmft"></a>.发布 DMFT 的 INF 文件示例

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

## <a name="example-frame-flow-with-a-uvc-device"></a>使用 UVC 设备的示例框架流

 (1) 的 Unstitched 组合帧 USBVdeo.sys：

![Unstitched 组合框](images/unstitched-combined.png)

 (2) 帧 unwarped，拼接，并转换为 DMFT 中的 equirectangular，该将发送到应用程序的呈现元素进行预览，并转换为要存储到文件的视频接收器或照片接收器：

![Frame unwarped、拼接和转换](images/unwarped-stitched-transformed.png)

 (3) 使用 UI 元素在应用程序中呈现的视区，该 UI 元素应用了一个球面投影，同时提供了视区旋转和视图交互字段：

![呈现的视区](images/rendered-viewport.png)