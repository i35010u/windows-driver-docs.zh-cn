---
title: WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES 是包含 Rx 合并卸载功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 17c008b6aa75b88f91ef66a0a3de239f7ca2b0b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818027"
---
# <a name="wdi_tlv_receive_coalesce_offload_capabilities"></a>WDI \_ TLV \_ 接收 \_ 联合 \_ 卸载 \_ 功能


WDI \_ tlv \_ 接收 \_ 合并 \_ 卸载 \_ 功能是包含 RX 合并卸载功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xCE

## <a name="length"></a>长度


以下值的大小 (以字节为单位) 。

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
<td>指定是否为 IPv4 启用 Rx 联合。
<p>有效值为 0 (未启用)  (启用 1) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否为 IPv6 启用 Rx 联合。
<p>有效值为 0 (未启用)  (启用 1) 。</p></td>
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

 

 




