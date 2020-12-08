---
title: WDI_TLV_POWER_STATE
description: WDI_TLV_POWER_STATE 是包含电源状态的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_POWER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 422b6be846cf785be6761c8d88995fb988c2cdce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834269"
---
# <a name="wdi_tlv_power_state"></a>WDI \_ TLV \_ 电源 \_ 状态


WDI \_ tlv \_ 电源 \_ 状态是包含电源状态的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x44

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>指定电源状态。
<p>有效值是：</p>
<ul>
<li>0x0001：退出低功耗 (D0) </li>
<li>0x0003：输入低功耗 (D2) </li>
<li>0x0004： (D3 进入关机状态，在某些平台上实际可能没有断电) </li>
</ul></td>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




