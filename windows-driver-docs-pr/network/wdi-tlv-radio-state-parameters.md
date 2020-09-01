---
title: WDI_TLV_RADIO_STATE_PARAMETERS
description: WDI_TLV_RADIO_STATE_PARAMETERS 是包含 OID_WDI_TASK_SET_RADIO_STATE 的无线电状态参数的 TLV。
ms.assetid: D977DF8A-146C-4921-AE7C-5FBEC7FBA4C8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RADIO_STATE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c0363353408e191f3b7a0b467e5c447d6bf177c9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214252"
---
# <a name="wdi_tlv_radio_state_parameters"></a>WDI \_ TLV \_ 无线电 \_ 状态 \_ 参数


WDI \_ tlv \_ 无线电 \_ 状态 \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ 任务 \_ 集 \_ 无线电 \_ 状态](./oid-wdi-task-set-radio-state.md)的无线电状态参数。

## <a name="tlv-type"></a>TLV 类型


0xA0

## <a name="length"></a>Length


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>所需的无线电状态。
<p>有效值为 0 (无线电关闭) 和 1 (启用了无线电) 。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

