---
title: 相机控件属性
description: 相机控件属性
ms.assetid: 36a57245-e89e-4418-b0c4-a4c1479413b2
keywords:
- 照相机控件属性 WDK 视频捕获
- 控件属性 WDK 视频捕获
- PROPSETID_VIDCAP_CAMERACONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f1de07d7f9e7aa29fbbd069823523fede34c63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386674"
---
# <a name="camera-control-properties"></a>相机控件属性


[PROPSETID\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)属性集包含与相关的视频照相机控件的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_CAMERACONTROL 属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_CAMERACONTROL KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXPOSURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure)"><strong>KSPROPERTY_CAMERACONTROL_EXPOSURE</strong></a></p></td>
<td><p>控制照相机的数字的暴露时间。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus)"><strong>KSPROPERTY_CAMERACONTROL_FOCUS</strong></a></p></td>
<td><p>控制设置的照相机的焦点。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IRIS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris)"><strong>KSPROPERTY_CAMERACONTROL_IRIS</strong></a></p></td>
<td><p>控制照相机的 aperture 设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ZOOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom)"><strong>KSPROPERTY_CAMERACONTROL_ZOOM</strong></a></p></td>
<td><p>控制照相机的缩放设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PAN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan)"><strong>KSPROPERTY_CAMERACONTROL_PAN</strong></a></p></td>
<td><p>控件的照相机的平移设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ROLL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll)"><strong>KSPROPERTY_CAMERACONTROL_ROLL</strong></a></p></td>
<td><p>控件的照相机的滚动更新设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_TILT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt)"><strong>KSPROPERTY_CAMERACONTROL_TILT</strong></a></p></td>
<td><p>控件的照相机的倾斜设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-scanmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_SCANMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-scanmode)"><strong>KSPROPERTY_CAMERACONTROL_SCANMODE</strong></a></p></td>
<td><p>控制照相机的传感器，例如交错，或非交错的扫描模式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-privacy" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PRIVACY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-privacy)"><strong>KSPROPERTY_CAMERACONTROL_PRIVACY</strong></a></p></td>
<td><p>控制是否应捕获视频中，相机传感器，或阻止捕获视频。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PANTILT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt)"><strong>KSPROPERTY_CAMERACONTROL_PANTILT</strong></a></p></td>
<td><p>控制照相机的绝对平移和倾斜设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PAN_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan-relative)"><strong>KSPROPERTY_CAMERACONTROL_PAN_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对从其当前值的垂直轴旋转。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_TILT_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt-relative)"><strong>KSPROPERTY_CAMERACONTROL_TILT_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对从其当前位置的水平轴旋转。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll-relative)"><strong>KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对映像查看从其当前值的轴旋转。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom-relative)"><strong>KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对缩放设置从其当前值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure-relative)"><strong>KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对快门速度从其当前值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris-relative)"><strong>KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE</strong></a></p></td>
<td><p>指定照相机的相对 aperture 设置从其当前值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus-relative)"><strong>KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对焦点设置从其当前值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt-relative)"><strong>KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE</strong></a></p></td>
<td><p>控制照相机的相对平移和倾斜设置从其当前值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focal-length" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focal-length)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH</strong></a></p></td>
<td><p>指定照相机的焦点长度。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-auto-exposure-priority" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-auto-exposure-priority)"><strong>KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY</strong></a></p></td>
<td><p>指定设备是否可以动态更改帧速率。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows8-extended-camera-control-properties"></a>Windows 8 扩展相机控件属性


从 Windows 8 开始，对于要获取或设置照相机的控制设置的用户模式下客户端支持这些附加属性。 有关详细信息，请参阅[扩展相机控件属性](extended-camera-control-properties.md)并[如何对实现扩展相机控件属性](how-to-implement-extended-camera-control-properties.md)。

| PROPSETID\_VIDCAP\_CAMERACONTROL KS 属性                                                                                           | 属性说明                                                                                                  |
|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**KSPROPERTY\_CAMERACONTROL\_闪存\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-flash-property)                                         | 用户模式下客户端可以选择使用此属性获取或设置照相机的闪存控制特性。                |
| [**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-image-pin-capability-property)         | 用户模式下客户端使用此属性来确定是否照相机的图像插针和记录 pin 是互相排斥。 |
| [**KSPROPERTY\_CAMERACONTROL\_区域\_OF\_感兴趣\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-region-of-interest-property)             | 用户模式下客户端可以选择使用此属性获取或设置感兴趣特征的照相机的区域。           |
| [**KSPROPERTY\_CAMERACONTROL\_视频\_稳定\_模式\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-video-stabilization-mode-property) | 用户模式下客户端可以选择使用此属性获取或设置照相机的视频防抖动特征。          |

 

## <a href="" id="win8-1-extended-props"></a>Windows 8.1 扩展相机控件属性


从 Windows 8.1 [KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)属性集为照相机照片序列化提供了其他控件。 有关如何实现这些控件的详细信息，请参阅以下主题：

-   [扩展的照相机控件属性](extended-camera-control-properties.md)
-   [如何实现扩展的照相机控件属性](how-to-implement-extended-camera-control-properties.md)
-   [扩展的照相机控件有效负载](extended-camera-control-payloads.md)
-   [照片序列模式](photo-sequence-mode.md)

 

 




