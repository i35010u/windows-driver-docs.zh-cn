---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE
description: 闪存属性控件设置这两个正常的闪存模式下操作和序列的相机的照片模式。
ms.assetid: A190CB91-0AC4-4ECC-8C55-F0C48CF7B190
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8c404292ba7d4282de28bad588cd35b42a87b76c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522074"
---
# <a name="kspropertycameracontrolextendedflashmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE


闪存属性控件设置这两个正常的闪存模式下操作和序列的相机的照片模式。

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

 

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含一个或多个以下的按位 OR 组合闪存驱动程序支持的模式。

| 闪光模式                                           | 描述                                                                |
|------------------------------------------------------|----------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_闪存\_OFF                   | Flash 处于关闭状态。                                                              |
| KSCAMERA\_EXTENDEDPROP\_闪存\_ON                    | Flash 上处于默认强度级别。                                |
| KSCAMERA\_EXTENDEDPROP\_闪存\_ON\_ADJUSTABLEPOWER   | Flash 上处于特定电源级别。                                     |
| KSCAMERA\_EXTENDEDPROP\_闪存\_自动                  | Flash 是自动的基于光照条件。                           |
| KSCAMERA\_EXTENDEDPROP\_闪存\_自动\_ADJUSTABLEPOWER | Flash 是自动基于在特定电源级别光照条件。 |

 

可与以前的闪存设置除外 KSCAMERA 结合使用以下功能标志\_EXTENDEDPROP\_闪存\_OFF。

| Flash 功能 | 描述 |
|---|---|
| KSCAMERA\_EXTENDEDPROP\_闪存\_REDEYEREDUCTION | 启用红眼缩减功能。 此标志可以与任何其他设置组合。 |
| KSCAMERA\_EXTENDEDPROP\_FLASH\_SINGLEFLASH | 设置闪存只有一个触发器。 照相机未处于照片序列模式时，将忽略此功能。 |
| KSCAMERA\_EXTENDEDPROP\_闪存\_MULTIFLASHSUPPORTED | 每个序列帧设置闪存的触发器。 照相机未处于照片序列模式时，将忽略此功能。 |

 

**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含当前设置为照相机的闪存模式。

用于相机的默认闪存模式是 KSCAMERA\_EXTENDEDPROP\_闪存\_OFF。 如果照相机支持 flash，KSCAMERA\_EXTENDEDPROP\_闪存\_关闭 KSCAMERA\_EXTENDEDPROP\_FLASH\_ON 和 KSCAMERA\_EXTENDEDPROP\_闪存\_自动将所需的模式。 KSCAMERA\_EXTENDEDPROP\_闪存\_自动\_ADJUSTABLEPOWER 和 KSCAMERA\_EXTENDEDPROP\_FLASH\_自动\_ADJUSTABLEPOWER 模式可选。

照相机支持照片顺序模式，则闪存控件属性是否需要支持 KSCAMERA\_EXTENDEDPROP\_闪存\_SINGLEFLASH。

此属性控制是同步的不取消。

## <a name="remarks"></a>备注

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
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0XFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>尺寸</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>支持的闪存模式值。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>（当前闪存模式值设置） |（闪存功能标志）</td>
</tr>
</tbody>
</table>

 

Torch 模式时 KSCAMERA\_EXTENDEDPROP\_闪存\_ON\_ADJUSTABLEPOWER 或 KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER**Value.ull**的成员[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)包含强度的级别值介于 0-100。 强度为 0 表示最小级别，强度为 100 表示最高亮度级别。 如果未设置的可调整 power 标志中, 返回规范化的强度设置的值**Value.ull**。

如果无闪存模式之前设置，然后**标志**设置为 KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF （默认）。

### <a name="setting-the-property"></a>将属性设置

设置该属性是，KSPROPERTY\_类型\_集请求**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)将包含要设置的 torch 模式。 **Value.ull**的成员[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)将包含要设置的强度级别**标志**是 KSCAMERA\_EXTENDEDPROP\_FLASH\_ON\_ADJUSTABLEPOWER 或 KSCAMERA\_EXTENDEDPROP\_FLASH\_自动\_ADJUSTABLEPOWER。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
