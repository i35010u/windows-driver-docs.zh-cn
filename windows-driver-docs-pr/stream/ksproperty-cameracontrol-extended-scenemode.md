---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE
description: 场景模式属性选择驱动程序定义的模式，该模式表示预设控件的集合。
ms.assetid: 32C350FF-AA54-4F28-8AD2-341A31648B60
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ff76b779c92e09f8e28b7c1e695d49981a8f8fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823957"
---
# <a name="ksproperty_cameracontrol_extended_scenemode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE

场景模式属性选择驱动程序定义的模式，该模式表示预设控件的集合。 驱动程序确定分配到场景模式的预设，并在选定场景时启用这些控制设置。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 **KSCAMERA\_EXTENDEDPROP\_值**是必需的，但**值**成员被忽略。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含驱动程序支持的下列一种或多种场景模式的按位 "或" 组合。

| 场景模式                                       | 描述                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自动          | 自动气味模式。 控件处于自动设置状态。            |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_宏         | 宏场景模式（已定义驱动程序）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_纵向      | 纵向场景模式（已定义驱动程序）。                                 |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_运动         | 运动场景模式（已定义驱动程序）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_雪          | 雪场景模式（已定义驱动程序）。                                     |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_夜         | 夜间场景模式（驱动程序已定义）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_海滩         | 海滩场景模式（已定义驱动程序）。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_日落        | 日落场景模式（已定义驱动程序）。                                   |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_CANDLELIGHT   | Candlelight 场景模式（已定义驱动程序）。                              |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_横向     | 横向场景模式（已定义驱动程序）。                                |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_NIGHTPORTRAIT | 晚上纵向场景模式（已定义驱动程序）。                           |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_BACKLIT       | Backlit 场景模式（已定义驱动程序）。                                  |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_手册        | 控件是手动更改的，未设置预定义的场景模式。 |

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的场景模式。 照相机的默认场景模式始终是 KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自动。

此属性控件是异步的，不可取消。

## <a name="remarks"></a>备注

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
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（支持的场景模式值）。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前场景模式值设置（仅一个值）。</td>
</tr>
</tbody>
</table>

如果以前未设置任何场景模式，则**Flags**设置为 KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO （默认值）。

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET 请求， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要启用的场景模式。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
