---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据
description: 客户端使用此扩展属性控件查询驱动程序的元数据缓冲区要求。
ms.assetid: 6196DFF6-050A-4916-A188-70A89B60B5EA
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 83aa435a65b0625fae753698d905ff0c43a30c4f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188141"
---
# <a name="ksproperty_cameracontrol_extended_metadata"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据

客户端使用此扩展属性控件查询驱动程序的元数据缓冲区要求。 它连同标准 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构一起发送到驱动程序，后跟 [**KSCAMERA \_ EXTENDEDPROP \_ METADATAINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo) 结构。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控制</th>
<th>类型</th>
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

下面是可放置在 **KSCAMERA \_ EXTENDEDPROP 标头中的元数据标志 \_ 。标志** 字段。

```cpp
#define KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY                     0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED                0x0000000000000100
```

在 **Get** 调用中，驱动程序会执行以下操作：

1.  填充 **KSCAMERA \_ EXTENDEDPROP \_ 标头。功能** 为0。

2.  Fill KSCAMERA \_ EXTENDEDPROP \_ 标头。带有以上 KSCAMERA \_ EXTENDEDPROP \_ 元数据 XXX 标志的组合的标志 \_ *XXX* ，用于指示元数据内存要求。

3.  填充 KSCAMERA \_ EXTENDEDPROP \_ METADATAINFO。具有所需内存对齐 (KSCAMERA \_ EXTENDEDPROP \_ MetadataAlignment \_ *Xxx*) 的 BufferAlignment。 有关可能的值，请参阅 [**KSCAMERA \_ EXTENDEDPROP \_ MetadataAlignment**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_metadataalignment) 。

4.  填充 **KSCAMERA \_ EXTENDEDPROP \_ METADATAINFO。MaxMetadataBufferSize** ，具有所需的元数据缓冲区大小（以字节为单位）。

下表包含在使用元数据控件时 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>此 ID 必须是与其帧包含元数据的 pin 关联的 Pin ID。 这可以是任何预览、记录和图像 pin。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_METADATAINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)"><strong>KSCAMERA_EXTENDEDPROP_METADATAINFO</strong></a>) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这指示上次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这是未使用的，必须为0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是 <strong>KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED</strong> 或 KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY 的任意组合。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要求

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