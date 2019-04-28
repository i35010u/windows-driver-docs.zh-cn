---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式
description: KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式是用于打开和关闭人脸身份验证的属性 ID。
ms.assetid: 240AABDB-585B-462E-B391-1CB55BA563D5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 53c77198cd2eb297a3bee8cc5890e3bd35186789
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348026"
---
# <a name="kspropertycameracontrolextendedfaceauthmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式


**KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式**用于打开和关闭人脸身份验证的属性 id。

### <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Pin</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

 

以下位标志控制人脸身份验证驱动程序中：

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED                        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION  0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION          0x0000000000000004
```

下表介绍了标记功能：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong></p></td>
<td><p>可选功能。</p>
<p>指定时，驱动程序中禁用视频人脸身份验证模式。 此标志是与互斥<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>并<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>标志。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong></p></td>
<td><p>必需功能如果<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>不受支持。</p>
<p>指定时，为强制设置<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>上每个示例如帧元数据中所述。 此标志是与互斥<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong>并<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong>标志。 在此模式下应为每个帧捕获备用 IR strobe 开/关。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
<td><p>必需功能如果<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>不受支持。</p>
<p>此标志是与互斥<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>并<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong>标志。 在此模式下它应与后台环境 IR 光线减去创建红外线 （ir） 映像。</p></td>
</tr>
</tbody>
</table>

 

默认情况下，该驱动程序应具有**KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式**设置为**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式下\_禁用**如果它是常规用途 IR 照相机。 否则它应设置为**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_后台\_减法**或**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_替代\_帧\_照明**。

IR 照相机应该播发**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_禁用**如果需要适用于除 Windows Hello 的常规方案。

使用人脸登录名的红外线 （ir） 照相机应支持这两**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_替代\_帧\_照明**或**KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_后台\_减法**它们仅应不支持这些标志之一的功能两者。

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用的控件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须在筛选器的仅一个插针上播发。 Pin 必须为类型<strong>PINNAME_VIDEO_CAPTURE</strong>或<strong>PINNAME_VIDEO_PREVIEW</strong>，必须生成红外线 （ir） 传感器数据，并可共享对于 FrameServer 标记。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是<strong>sizeof</strong>(<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + <strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/dn567566" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567566)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>).</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是受支持的位 OR <strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong>上面定义的标志。</p>
<p>该驱动程序不应将同时播发<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>和<strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是任一<strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong>上面定义的标志。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
