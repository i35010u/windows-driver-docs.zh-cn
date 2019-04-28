---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_WHITEBALANCEMODE
description: 白平衡模式属性指定是否自动处理发生在白平衡或改为使用手动温度值。
ms.assetid: 5DEC4A56-3868-40AF-9FD0-CDB0637B875A
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03ec84ea1d613ae1be4f620ebe67856630cf784a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341833"
---
# <a name="kspropertycameracontrolextendedwhitebalancemode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_WHITEBALANCEMODE

白平衡模式属性指定是否自动处理发生在白平衡或改为使用手动温度值。

## <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING). **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含一个或多个以下的按位 OR 组合视频处理选项。

| 处理模式                               | 描述                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO   | 照相机驱动程序使用其自己的处理逻辑的视频。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_MANUAL | 照相机的驱动程序使用预设的处理方法或基于温度方法。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK   | 当前的视频处理方法已被锁定。                               |

**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含当前设置为照相机的视频处理标志。 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动设置可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁。

此属性控制是异步的不取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO  
这表示自动处理的支持。 该驱动程序将使用其内部逻辑以优化视频处理。 有关 KSPROPERTY\_类型\_GET 请求**VideoProc**的成员[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)必须包含视频处理的当前驱动程序确定值。 在白平衡的情况下，它必须包含开氏当前温度。 **模式下**成员将被忽略的自动操作。

此标志可能结合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_作为按位 OR 值的锁。 锁定时，照相机驱动程序的预期的行为是集中于白平衡并锁定为聚合值，不自动白平衡到再次尝试，直到收到新的白平衡命令的白平衡值。

锁定，而不合并 Auto 模式中，已锁定的控件应被不视为执行任何操作由照相机驱动程序。 在 Auto 模式下的组合中的锁定，已锁定的控件应触发新的聚合。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_MANUAL**  
-   手动指示对此视频处理所提供的特定值。 在白平衡的情况下如果**模式下**的成员[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)指示 KSCAMERA\_EXTENDEDPROP\_WHITEBALANCE\_温度**VideoProc.Value.ul**将包含以开氏度为单位的温度值。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK**
-   锁选项标志指示当前的视频处理已锁定到当前编写的任何值。 例如，应用程序可能会请求 auto 模式，直到确定特定的白平衡，此时应用程序将决定采用所有这些都有相同的白平衡设置的一系列照片。 在这种情况下，应用程序可能会指定 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁定标志。 照相机的驱动程序将确保白平衡信息不会更改跨不同的照片。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求，该驱动程序设置的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)到以下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Version</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0XFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>大小</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（支持的视频处理模式）</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前的视频处理模式。</td>
</tr>
</tbody>
</table>

如果以前设置无白平衡模式，则该驱动程序设置**标志**到 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动 （默认值）。 成员[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构，它遵循[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)根据处理模式的要求设置。

### <a name="setting-the-property"></a>将属性设置

设置该属性是，KSPROPERTY\_类型\_集请求**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)将包含要设置的白平衡模式。 **VideoProc.Value**的成员[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)必须时忽略**标志**包含 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动模式标志。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)

[**KSPROPERTY\_CAMERACONTROL\_扩展\_EXPOSUREMODE**](ksproperty-cameracontrol-extended-exposuremode.md)
