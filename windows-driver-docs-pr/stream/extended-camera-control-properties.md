---
title: 扩展的相机控件属性
description: 扩展相机控制接口用于在映像捕获期间控制相机功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf9ebeceabe7da5d0090f99e2f2768faca9d85c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839205"
---
# <a name="extended-camera-control-properties"></a>扩展的相机控件属性


从 Windows 8 开始提供的扩展相机控制界面用于在映像捕获期间控制相机功能。 驱动程序可以控制以下相机功能：

-   照相机的闪烁
-   图像 pin 和记录 pin 是否互相排斥
-   映像中的相关区域
-   视频抖动

驱动程序还可以选择以异步方式执行照相机控件操作，也就是说，在第一个请求完成之前，对某个操作的所有请求都将被拒绝。 如果驱动程序已成功执行异步照相机控制操作，它应触发 [**KSEVENTSETID \_ CameraAsyncControl**](./kseventsetid-cameraasynccontrol.md) 事件。 有关详细信息，请参阅 [**KSPROPERTY \_ CAMERACONTROL \_ \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s_ex) 。

UWP 应用可以访问这些属性来配置照相机：

## <a name="properties"></a>属性


<a href="" id="ksproperty-cameracontrol-flash-property"></a>[**KSPROPERTY \_ CAMERACONTROL \_ FLASH \_ 属性**](./ksproperty-cameracontrol-flash-property.md)  
用于打开或关闭照相机的闪烁，或将闪存置于自动模式。

<a href="" id="ksproperty-cameracontrol-image-pin-capability-property"></a>[**KSPROPERTY \_ CAMERACONTROL \_ IMAGE \_ 引脚 \_ 功能 \_ 属性**](./ksproperty-cameracontrol-image-pin-capability-property.md)  
用于标识照相机的图像 pin 和记录 pin 是否互相排斥。

<a href="" id="ksproperty-cameracontrol-region-of-interest-property"></a>[**KSPROPERTY \_ CAMERACONTROL \_ \_ \_ 感兴趣的区域 \_ 属性**](./ksproperty-cameracontrol-region-of-interest-property.md)  
用于获取或设置相机的感兴趣区域的特征。

<a href="" id="ksproperty-cameracontrol-video-stabilization-mode-property"></a>[**KSPROPERTY \_ CAMERACONTROL \_ 视频 \_ 稳定 \_ 模式 \_ 属性**](./ksproperty-cameracontrol-video-stabilization-mode-property.md)  
用于获取或设置照相机的视频抖动特征。

以下属性可从 Windows 8.1 开始使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-photomode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE</strong></a></p></td>
<td><p>用于获取或设置照相机的正常静止或照片序列模式。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photoframerate"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-photoframerate.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE</strong></a></p></td>
<td><p>当照相机的照片模式为序列模式时，用于获取当前照片捕获帧速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomaxframerate"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-photomaxframerate.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE</strong></a></p></td>
<td><p>用于获取或设置照相机处于照片序列模式时的最大捕获帧速率。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-phototriggertime"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME&lt;/strong&gt;](./ksproperty-cameracontrol-extended-phototriggertime.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME</strong></a></p></td>
<td><p>用于获取或设置照相机驱动程序的触发时间。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-warmstart"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART&lt;/strong&gt;](./ksproperty-cameracontrol-extended-warmstart.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART</strong></a></p></td>
<td><p>用于获取或设置热启动 (照相机就绪) 状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-maxvidfps-photores"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES&lt;/strong&gt;](./ksproperty-cameracontrol-extended-maxvidfps-photores.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES</strong></a></p></td>
<td><p>用于获取或设置视频捕获插针上特定分辨率可能的最大可能帧速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photothumbnail"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL&lt;/strong&gt;](./ksproperty-cameracontrol-extended-photothumbnail.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL</strong></a></p></td>
<td><p>用于获取或设置照相机的缩略图功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-scenemode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-scenemode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE</strong></a></p></td>
<td><p>用于获取或设置驱动程序定义的模式，该模式表示预设控件的集合。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-torchmode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-torchmode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE</strong></a></p></td>
<td><p>用于获取或设置一种方法，即在低亮度情况下使用摄像机的 flash。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-flashmode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-flashmode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE</strong></a></p></td>
<td><p>用于获取或设置照相机的正常和序列照片模式的 flash 模式操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-optimizationhint"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT&lt;/strong&gt;](./ksproperty-cameracontrol-extended-optimizationhint.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT</strong></a></p></td>
<td><p>用于获取或设置是对白平衡还是手动温度值进行自动处理。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-whitebalancemode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-whitebalancemode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE</strong></a></p></td>
<td><p>用于获取或设置照相机是否针对照片或视频操作进行了优化。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-exposuremode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-exposuremode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE</strong></a></p></td>
<td><p>用于获取或设置是使用自动处理进行公开还是使用手动时间值。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-focusmode"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE&lt;/strong&gt;](./ksproperty-cameracontrol-extended-focusmode.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE</strong></a></p></td>
<td><p>用于获取或设置照相机的 "自动"、"手动" 和 "预设" 焦点模式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-iso"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_ISO&lt;/strong&gt;](./ksproperty-cameracontrol-extended-iso.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_ISO</strong></a></p></td>
<td><p>用于获取或设置照相机的预设或自动 ISO 设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-fieldofview"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW&lt;/strong&gt;](./ksproperty-cameracontrol-extended-fieldofview.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW</strong></a></p></td>
<td><p>用于获取摄像机位置的视图和螺距角度的字段。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-evcompensation"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION&lt;/strong&gt;](./ksproperty-cameracontrol-extended-evcompensation.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION</strong></a></p></td>
<td><p>用于获取或设置暴露控制调整设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-cameraangleoffset"></a><a href="/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET&lt;/strong&gt;](./ksproperty-cameracontrol-extended-cameraangleoffset.md)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET</strong></a></p></td>
<td><p>用于获取摄像机位置的螺距和偏航角度。</p></td>
</tr>
</tbody>
</table>

 

这些结构和枚举支持扩展相机控制界面：

## <a name="structures"></a>結構


-   [**KSPROPERTY \_ CAMERACONTROL \_ \_ EX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s_ex)
-   [**KSPROPERTY \_ CAMERACONTROL \_ FLASH \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_flash_s)
-   [**KSPROPERTY \_ CAMERACONTROL \_ 图像 \_ PIN \_ 功能 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)
-   [**KSPROPERTY \_ CAMERACONTROL \_ \_ \_ \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s)
-   [**KSPROPERTY \_ CAMERACONTROL \_ VIDEOSTABILIZATION \_ 模式 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_videostabilization_mode_s)
-   [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA \_ MAXVIDEOFPS \_ FORPHOTORES**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA \_ EXTENDEDPROP \_ FIELDOFVIEW**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)

## <a name="enumerations"></a>枚举


-   [**KS \_ CameraControlAsyncOperation**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_cameracontrolasyncoperation)
-   [**KSEVENT \_ CAMERACONTROL**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksevent_cameracontrol)
-   [**KSPROPERTY \_ CAMERACONTROL \_ FLASH**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_flash)
-   [**KSPROPERTY \_ CAMERACONTROL \_ 图像 \_ PIN \_ 功能**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_image_pin_capability)
-   [**KSPROPERTY \_ CAMERACONTROL \_ \_ \_ 感兴趣的区域**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_region_of_interest)
-   [**KSPROPERTY \_ CAMERACONTROL \_ 视频 \_ 抖动 \_ 模式**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_video_stabilization_mode)

实现此接口的示例驱动程序代码在 [如何实现扩展相机控件属性](how-to-implement-extended-camera-control-properties.md)中提供。

