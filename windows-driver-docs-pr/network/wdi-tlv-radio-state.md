---
title: WDI_TLV_RADIO_STATE
description: WDI_TLV_RADIO_STATE 是一种 TLV，其中包含硬件和软件中的无线电状态。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f3bd3753cb606379f0b3d4bf4daca5e32e640543
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834255"
---
# <a name="wdi_tlv_radio_state"></a>WDI \_ TLV \_ 无线电 \_ 状态


WDI \_ tlv \_ 无线电 \_ 状态是一个 tlv，其中包含硬件和软件中的无线电状态。

## <a name="tlv-type"></a>TLV 类型


0xA1

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

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
<td>UINT8</td>
<td>硬件中的无线电的当前状态。
<p>有效值为0和1。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>软件中广播的当前状态。
<p>有效值为0和1。</p></td>
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

 

 




