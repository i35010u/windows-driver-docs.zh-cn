---
title: KSPROPERTY\_EXTXPORT\_状态
description: KSPROPERTY\_EXTXPORT\_状态属性设置或获取外部设备的传输模式和状态。
ms.assetid: c508b6ce-2a37-4fca-9edf-66700d9cbd15
keywords:
- KSPROPERTY_EXTXPORT_STATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cebb63463dc7c3c93c5d9ceae0f64aa0f8899d65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838054"
---
# <a name="ksproperty_extxport_state"></a>KSPROPERTY\_EXTXPORT\_状态


KSPROPERTY\_EXTXPORT\_状态属性设置或获取外部设备的传输模式和状态。

## <span id="ddk_ksproperty_extxport_state_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state" data-raw-source="[&lt;strong&gt;TRANSPORT_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state)"><strong>TRANSPORT_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种传输\_状态结构，用于描述外部传输的当前模式和状态。 例如，当模式设置为 "播放" 时，状态可能设置为 "冻结（暂停）"。

<a name="remarks"></a>备注
-------

KSPROPERTY\_EXTXPORT\_S 结构的**XPrtState**成员指定模式和状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

[**传输\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-transport_state)

 

 






