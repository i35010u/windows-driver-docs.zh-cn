---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ WHITEBALANCEMODE
description: "\"白平衡模式\" 属性指定是否对白平衡进行自动处理或改用手动温度值。"
ms.assetid: 5DEC4A56-3868-40AF-9FD0-CDB0637B875A
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE 流媒体设备
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
ms.openlocfilehash: 9247d96fb8b5230d152d49b89fe6b91867c4790b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191417"
---
# <a name="ksproperty_cameracontrol_extended_whitebalancemode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ WHITEBALANCEMODE

"白平衡模式" 属性指定是否对白平衡进行自动处理或改用手动温度值。

## <a name="usage-summary-table"></a>使用情况摘要表

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
<th>获取</th>
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
<td><p>筛选器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) 结构。

总属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个视频处理选项的按位 "或" 组合。

| 处理模式                               | 说明                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动   | 照相机驱动程序使用其自己的视频处理逻辑。                       |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ | 照相机驱动程序使用预设处理方法或基于温度的方法。 |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_   | 当前视频处理方法已锁定。                               |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的视频处理标志。 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO 设置可能与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG LOCK 组合在一起 \_ 。

此属性控件是异步的，不可取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动  
这表示支持自动处理。 驱动程序将使用其内部逻辑来优化视频处理。 对于 KSPROPERTY \_ 类型 \_ GET 请求， [**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的**VideoProc**成员必须包含当前驱动程序确定的视频处理值。 如果是白平衡，则必须包含当前的开氏温度。 自动操作将忽略 **模式** 成员。

此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG LOCK 组合 \_ 为按位 "或" 值。 锁定后，照相机驱动程序的预期行为是聚合到白平衡上，并将白色余额值锁定为聚合值，而不是再次尝试自动余额，直到收到新的白平衡命令。

锁定，如果不结合使用自动模式，照相机驱动程序应将已锁定的控件视为不能操作。 锁定与 Auto 模式结合使用时，已锁定的控件应会触发新的聚合。

**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_**  
-   手动指示对于此视频处理，提供了特定的值。 在进行白平衡的情况下，如果[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的**Mode**成员指示 KSCAMERA \_ EXTENDEDPROP \_ WHITEBALANCE \_ 温度，则**VideoProc**将包含温度值（开氏度）。

**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_**
-   锁定选项标志指示当前视频处理锁定为当前编程的任何值。 例如，应用程序可能会请求 "自动" 模式，直到确定特定的白余额为止，此时应用程序会决定采用一系列具有相同白平衡设置的照片。 在这种情况下，应用程序可以指定 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 锁定标志。 照相机驱动程序将确保白余额信息不会在不同照片上更改。

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

如果以前未设置白平衡模式，则驱动程序会将 **标志** 设置为 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO (默认) 。 按照处理模式的要求设置[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)后面的[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构的成员。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的白平衡模式。 当**Flags**包含 KSCAMERA **VideoProc.Value** EXTENDEDPROP VIDEOPROCFLAG AUTO mode 标志时，必须忽略[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)的 VideoProc 成员 \_ \_ \_ 。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EXPOSUREMODE**](ksproperty-cameracontrol-extended-exposuremode.md)