---
title: KSPROPERTY\_EXTXPORT\_状态\_通知
description: KSPROPERTY\_EXTXPORT\_状态\_通知属性设置或获取传输模式和状态更改的通知。
ms.assetid: 3ebf3806-bdec-4ea2-8f2a-e75314ee020a
keywords:
- KSPROPERTY_EXTXPORT_STATE_NOTIFY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_STATE_NOTIFY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63d82378846f6270dcd9047d4c3601b61da0b0a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838055"
---
# <a name="ksproperty_extxport_state_notify"></a>KSPROPERTY\_EXTXPORT\_状态\_通知


KSPROPERTY\_EXTXPORT\_状态\_通知属性设置或获取传输模式和状态更改的通知。

## <span id="ddk_ksproperty_extxport_state_notify_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_STATE_NOTIFY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

当传输状态发生更改时，属性值（操作数据）是描述当前外部传输的 KSPROPERTY\_EXTXPORT\_S 结构。

<a name="remarks"></a>备注
-------

当传输状态发生更改时，KSPROPERTY\_EXTXPORT\_S 结构将接收通知。

此调用是一个同步操作，将不会返回，直到传输状态发生更改。 不建议使用此方法，因为并非所有 DV 摄像机都可以支持此操作。

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

 

 






