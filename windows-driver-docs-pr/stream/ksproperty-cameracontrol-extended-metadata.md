---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_元数据
description: 此扩展的属性控制客户端用于查询元数据缓冲区要求的驱动程序。
ms.assetid: 6196DFF6-050A-4916-A188-70A89B60B5EA
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA 流式处理媒体设备
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
ms.openlocfilehash: 7d60f1b9a3652ddbc5bd211f3d0ece9e7a03ed1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356705"
---
# <a name="kspropertycameracontrolextendedmetadata"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_元数据

此扩展的属性控制客户端用于查询元数据缓冲区要求的驱动程序。 发送到标准以及驱动程序[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构跟[ **KSCAMERA\_EXTENDEDPROP\_与 METADATAINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)结构。

## <a name="usage-summary-table"></a>使用率摘要表

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

以下是可以放入的元数据标志**KSCAMERA\_EXTENDEDPROP\_标头。标志**字段。

```cpp
#define KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY                     0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED                0x0000000000000100
```

在中**获取**调用时，该驱动程序执行以下操作：

1.  填充**KSCAMERA\_EXTENDEDPROP\_标头。功能**0。

2.  填充 KSCAMERA\_EXTENDEDPROP\_标头。任意上述 KSCAMERA 组合的标志\_EXTENDEDPROP\_元数据\_*XXX*标志以指示元数据内存要求。

3.  填充 KSCAMERA\_EXTENDEDPROP\_与 METADATAINFO。使用所需的内存对齐方式的 BufferAlignment (KSCAMERA\_EXTENDEDPROP\_MetadataAlignment\_*Xxx*)。 请参阅[ **KSCAMERA\_EXTENDEDPROP\_MetadataAlignment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_extendedprop_metadataalignment)有关可能的值。

4.  填充**KSCAMERA\_EXTENDEDPROP\_与 METADATAINFO。MaxMetadataBufferSize**使用必需的元数据的缓冲区大小，以字节为单位。

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构时使用元数据控件字段。

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
<td><p>这必须是的固定的帧包含元数据与关联的 Pin ID。 这可以是任何预览、 录制和图像插针。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_METADATAINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)"><strong>KSCAMERA_EXTENDEDPROP_METADATAINFO</strong></a>)，</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这表示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这是未使用，必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是任何组合<strong>KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED</strong>或 KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY。</p></td>
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
