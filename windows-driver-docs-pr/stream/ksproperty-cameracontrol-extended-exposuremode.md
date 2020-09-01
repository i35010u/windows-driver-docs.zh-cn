---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EXPOSUREMODE
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
ms.openlocfilehash: 0432251c86a7d43cea044110e8df24eb05f1a949
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192639"
---
# <a name="ksproperty_cameracontrol_extended_exposuremode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EXPOSUREMODE

"公开控制" 属性指定是否进行自动处理以便公开或使用手动时间值。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|---|---|---|---|---|
| 是 | 是 | 筛选器 | [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) 结构。

总属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个视频处理选项的按位 "或" 组合。

| 处理模式                               | 说明                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动   | 照相机驱动程序使用其自己的视频处理逻辑。                       |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ | 照相机驱动程序使用预设的处理方法。                               |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_   | 当前视频处理方法已锁定。                               |

 

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的视频处理标志。 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO 设置可能与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG LOCK 组合在一起 \_ 。

此属性控件是异步的，可取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动  
这表示支持自动处理。 驱动程序将使用其内部逻辑来优化视频处理。 对于 KSPROPERTY \_ 类型 \_ GET 请求， [**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的**VideoProc**成员必须包含当前驱动程序确定的视频处理值。

此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG LOCK 组合 \_ 为按位 "或" 值。

锁定，如果不结合使用自动模式，照相机驱动程序应将已锁定的控件视为不能操作。 锁定与 Auto 模式结合使用时，已锁定的控件应会触发新的聚合。

此标志不得与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 手动组合。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_MANUAL"></span><span id="kscamera_extendedprop_videoprocflag_manual"></span>KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_  
手动指示对于此视频处理，提供了特定的值。 为驱动程序提供了特定的值。

此标志不得与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO 或 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ LOCK 结合。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_LOCK"></span><span id="kscamera_extendedprop_videoprocflag_lock"></span>KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_  
锁定选项标志指示当前视频处理锁定为当前编程的任何值。 例如，应用程序可能会请求自动模式，直至确定特定的暴露程度。 此时，应用程序将决定采用一系列照片，所有这些都具有相同的曝光。 在这种情况下，应用程序可以指定 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 锁定标志。 

此标志不得与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 手动组合。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 的成员设置为以下项。

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
<td> (0xFFFFFFFF) KSCAMERA_EXTENDEDPROP_FILTERSCOPE。</td>
</tr>
<tr class="odd">
<td>大小</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) </p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |支持 (视频处理模式) </td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前视频处理模式。</td>
</tr>
</tbody>
</table>

 

如果以前未设置任何曝光模式，则驱动程序会将 **标志** 设置为 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO (默认) 。 按照处理模式的要求设置[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)后面的[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构的成员。

当**VideoProp.Value.ull** MODE 为 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO 时，VideoProp. u) 值必须包含当前的曝光设置。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的曝光模式。 当**Flags**包含 KSCAMERA **VideoProc.Value** EXTENDEDPROP VIDEOPROCFLAG AUTO mode 标志时，必须忽略[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的 VideoProc 成员 \_ \_ \_ 。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[KSCAMERA \_ EXTENDEDPROP \_ 标头](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)