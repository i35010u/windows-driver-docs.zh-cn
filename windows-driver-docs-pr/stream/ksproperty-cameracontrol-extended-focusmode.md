---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSMODE
description: 焦点模式属性控制照相机的 "自动"、"手动" 和 "预设" 焦点模式。
ms.assetid: FA014A4B-0CD3-4288-B721-4A73CDD28551
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0cb4fcf43eba200b599826edf2ff9ee5ab12124d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190531"
---
# <a name="ksproperty_cameracontrol_extended_focusmode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSMODE

焦点模式属性控制照相机的 "自动"、"手动" 和 "预设" 焦点模式。

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

| 处理和焦点模式                        | 描述                                                                  |
|--------------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动      | 照相机驱动程序使用其自己的视频处理逻辑。                       |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_    | 照相机驱动程序使用预设处理方法或基于温度的方法。 |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_      | 当前视频处理方法已锁定。                               |
| KSCAMERA \_ EXTENDEDPROP \_ \_        | 没有聚合焦点集。                                               |
| KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ 宏      | 宏范围焦点。                                               |
| KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ 法线     | 正常范围焦点焦点。                                              |
| KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ FULLRANGE  | 完全范围焦点。                                                |
| KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ 无限大   | 无限范围焦点焦点。                                            |
| KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ HYPERFOCAL | Hyperfocal 范围。                                                            |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的视频处理标志。 如果 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO 设置可以与 KSCAMERA \_ EXTENDEDPROP VIDEOPROCFLAG LOCK 组合在一起 \_ \_ 。

此属性控件是异步的，可取消。

## <a name="remarks"></a>备注

### <a name="processing-modes"></a>处理模式

**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动**

此标志指示在触发完成事件时自动焦点操作已聚合。 完成后，如果此标志不是与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG 锁结合使用 \_ ，则焦点可能会发生分叉，照相机驱动程序可能会继续尝试会合。 如果包含 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 标记，焦点将锁定到第一次聚合，并且不会更改，直到接收到新的焦点命令。

锁定，如果不结合使用自动模式，照相机驱动程序应将已锁定的控件视为不能操作。 锁定与 Auto 模式结合使用时，已锁定的控件应会触发新的聚合。

此标志与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 和 KSCAMERA \_ EXTENDEDPROP \_ 聚焦 \_ 连续标志互斥。

**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_**

手动指示对于此视频处理，提供了特定的值。 为驱动程序提供了特定的值。

不能将此标志与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO、KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ LOCK 或 KSCAMERA \_ EXTENDEDPROP \_ 集中 \_ 在一起。

**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_**

如果设置此标志时未使用相应的 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动标志，则照相机驱动程序应锁定当前焦点状态并在锁定焦点后触发完成事件。 照相机驱动程序不得改变焦点状态，直到接收到新的焦点命令。 如果 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ 自动组合此标志，照相机驱动程序将汇聚为自动焦点，并将焦点锁定到该聚合点，然后触发完成事件。 此标志不得与 KSCAMERA \_ EXTENDEDPROP \_ FOCUS \_ 连续流或 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ MANUAL 结合。

不能将此标志与焦点控件的范围标志一起指定，除非它与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG AUTO 结合使用 \_ 。 在这种情况下，将使用范围标志来执行焦点，以确定尝试自动搜索的位置。 然后，在聚合时，焦点设置锁和完成事件将激发。

**KSCAMERA \_ EXTENDEDPROP \_ \_**

此标志指示焦点是连续的。 在这种情况下，焦点控制没有单个会合点。 驱动程序必须接受此请求并立即完成异步操作。

此标志不得与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO、KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ LOCK 或 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ MANUAL 结合。

所有驱动程序都需要此模式。

**KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ 宏**

此标志指示应为宏范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO and KSCAMERA \_ EXTENDEDPROP \_ FOCUS 连续组合 \_ 。

**KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ 法线**

此标志指示应为正常范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO and KSCAMERA \_ EXTENDEDPROP \_ FOCUS 连续组合 \_ 。

**KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ FULLRANGE**

此标志指示应为整个范围执行焦点收敛。 确切的焦点范围取决于驱动程序。 此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO and KSCAMERA \_ EXTENDEDPROP \_ FOCUS 连续组合 \_ 。

所有驱动程序都需要此模式。

**KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ 无限大**

此标志指示应为无限范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO and KSCAMERA \_ EXTENDEDPROP \_ FOCUS 连续组合 \_ 。

**KSCAMERA \_ EXTENDEDPROP \_ 焦点 \_ 范围 \_ HYPERFOCAL**

此标志指示应为 hyperfocal 范围执行焦点聚合。 确切的焦点范围取决于驱动程序。 此标志可以与 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO and KSCAMERA \_ EXTENDEDPROP \_ FOCUS 连续组合 \_ 。

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
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE |</p>
<p>支持 (视频处理和焦点模式) </p></td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前视频处理和焦点模式。</td>
</tr>
</tbody>
</table>


如果以前未设置焦点范围标志，则驱动程序会将 **标志** 设置为 KSCAMERA \_ EXTENDEDPROP \_ focus \_ RANGE FULLRANGE，并将 \_ KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO (默认) 。 按照焦点模式的要求设置[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)后面的[**KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构的成员。

当**VideoProp.Value.ull** MODE 为 KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG \_ AUTO 时，VideoProp. u) 值必须包含当前的曝光设置。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的焦点模式。 当**Flags**包含 KSCAMERA EXTENDEDPROP VIDEOPROCFLAG **VideoProc.Value** [** \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) \_ \_ \_ AUTO，KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCFLAG KSCAMERA \_ ，EXTENDEDPROP \_ \_ 聚焦 \_ 连续标志时，必须忽略 KSCAMERA EXTENDEDPROP VIDEOPROCSETTING 的 VideoProc 成员。

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