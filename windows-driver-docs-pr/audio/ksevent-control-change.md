---
title: KSEVENT \_ 控件 \_ 更改
description: KSEVENT \_ 控件 \_ 更改事件指示在表示硬件卷控制旋钮、静音开关或其他类型手动控制的节点上发生了控件值更改。使用情况摘要 TableTargetEvent 描述符 TypeEvent 值 TypePinKSE \_ NODEKSEVENTDATA (操作数据的事件值类型) 是一个 KSEVENTDATA 结构，它指定要用于事件的通知类型。
ms.assetid: 32d8e14c-f21d-4bac-8d98-8aca40e30b60
keywords:
- KSEVENT_CONTROL_CHANGE 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_CONTROL_CHANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720846545ffec49b9ebee2eda7fb391273ca45ea
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102680"
---
# <a name="ksevent_control_change"></a>KSEVENT \_ 控件 \_ 更改


KSEVENT \_ 控件 \_ 更改事件指示在表示硬件卷控制旋钮、静音开关或其他类型手动控制的节点上发生了控件值更改。

**使用情况摘要表**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标</th>
<th align="left">事件描述符类型</th>
<th align="left">事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的事件值类型是一个 KSEVENTDATA 结构，它指定要用于事件的通知类型。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSE \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)

[**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**PCEVENT \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)

[**PCEVENT \_ 请求**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)

[IPortEvents](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)

