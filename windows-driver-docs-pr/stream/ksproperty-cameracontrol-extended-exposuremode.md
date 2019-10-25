---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_EXPOSUREMODE
description: "\"公开控制\" 属性指定是否进行自动处理以便公开或使用手动时间值。"
ms.assetid: 54D4F286-09F2-48B5-9A7A-9445999972BD
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7ceca5a9fe3e0c53e670f6e39b6dd02292b35380
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843240"
---
# <a name="ksproperty_cameracontrol_extended_exposuremode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_EXPOSUREMODE

"公开控制" 属性指定是否进行自动处理以便公开或使用手动时间值。

## <a name="usage-summary-table"></a>使用情况摘要表

| “获取” | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|---|---|---|---|---|
| “是” | “是” | Filter | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个视频处理选项的按位 "或" 组合。

| 处理模式                               | 描述                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动   | 照相机驱动程序使用其自己的视频处理逻辑。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册 | 照相机驱动程序使用预设的处理方法。                               |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁   | 当前视频处理方法已锁定。                               |

 

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的视频处理标志。 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动设置可能与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK 结合在一起。

此属性控件是异步的，可取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自动  
这表示支持自动处理。 驱动程序将使用其内部逻辑来优化视频处理。 对于 KSPROPERTY\_类型\_GET 请求， [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的**VideoProc**成员必须包含当前驱动程序确定的视频处理值。

此标志可以与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁定作为按位 "或" 值组合。

锁定，如果不结合使用自动模式，照相机驱动程序应将已锁定的控件视为不能操作。 锁定与 Auto 模式结合使用时，已锁定的控件应会触发新的聚合。

此标志不得与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册结合。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_MANUAL"></span><span id="kscamera_extendedprop_videoprocflag_manual"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册  
手动指示对于此视频处理，提供了特定的值。 为驱动程序提供了特定的值。

此标志不得与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 或 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_LOCK 结合。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_LOCK"></span><span id="kscamera_extendedprop_videoprocflag_lock"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁  
锁定选项标志指示当前视频处理锁定为当前编程的任何值。 例如，应用程序可能会请求自动模式，直至确定特定的暴露程度。 此时，应用程序将决定采用一系列照片，所有这些都具有相同的曝光。 在这种情况下，应用程序可以指定 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_锁定标志。 

此标志不得与 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手册结合。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求时，驱动程序会将[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（支持视频处理模式）</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前视频处理模式。</td>
</tr>
</tbody>
</table>

 

如果以前未设置任何曝光模式，则驱动程序会将**标志**设置为 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO （默认值）。 [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构的成员将按照处理模式的要求设置[ **\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。

当 mode 为 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO 时， **u)** 值必须包含当前的曝光设置。

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET 请求， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的曝光模式。 当**Flags**包含 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO mode 标志时，必须忽略[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的**VideoProc**成员。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr>
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[KSCAMERA\_EXTENDEDPROP\_标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
