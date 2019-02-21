---
title: KSPROPERTY\_BDA\_CA\_智能\_卡\_状态
description: 客户端使用 KSPROPERTY\_BDA\_CA\_智能\_卡\_状态以确定与 ECM 映射节点关联的智能卡读取器的状态。
ms.assetid: a53cea17-0463-4909-839b-6e8ad67dac82
keywords:
- KSPROPERTY_BDA_CA_SMART_CARD_STATUS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_SMART_CARD_STATUS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbb2b0febc584761a69bb84ff842e47cf3002d67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534453"
---
# <a name="kspropertybdacasmartcardstatus"></a>KSPROPERTY\_BDA\_CA\_智能\_卡\_状态


客户端使用 KSPROPERTY\_BDA\_CA\_智能\_卡\_状态以确定与 ECM 映射节点关联的智能卡读取器的状态。

## <span id="ddk_ksproperty_bda_ca_smart_card_status_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_SMART_CARD_STATUS_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定的智能卡读取器状态。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSEVENT\_BDA\_CA\_智能\_卡\_状态\_已更改**](ksevent-bda-ca-smart-card-status-changed.md)

[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






