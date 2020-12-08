---
title: WDI_TLV_ASSOCIATION_RESULT
description: WDI_TLV_ASSOCIATION_RESULT 是包含关联结果的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESULT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fc3e6494ce3ed329a9b775154fc216175dc13541
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817071"
---
# <a name="wdi_tlv_association_result"></a>WDI \_ TLV \_ 关联 \_ 结果


WDI \_ tlv \_ 关联 \_ 结果是包含关联结果的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x35

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                       | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                 |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ BSSID**](wdi-tlv-bssid.md)                                                   |                                |          | BSS 的 BSSID。                                                                                                                                                                                       |
| [**WDI \_ TLV \_ 关联 \_ 结果 \_ 参数**](wdi-tlv-association-result-parameters.md) |                                |          | 关联结果参数。                                                                                                                                                                          |
| [**WDI \_ TLV \_ 关联 \_ 请求 \_ 帧**](wdi-tlv-association-request-frame.md)         |                                | X        | 用于关联的关联请求。 这不包括 802.11 MAC 标头。                                                                                                         |
| [**WDI \_ TLV \_ 关联 \_ 响应 \_ 帧**](wdi-tlv-association-response-frame.md)       |                                | X        | 收到的关联响应。 这不包括 802.11 MAC 标头。                                                                                                                    |
| [**WDI \_ TLV \_ 身份验证 \_ 响应 \_ 帧**](wdi-tlv-authentication-response-frame.md) |                                | X        | 收到的身份验证响应，出现故障代码。 这不包括 802.11 MAC 标头。 仅当在身份验证交换期间连接尝试失败时，才应包括此方法。 |
| [**WDI \_ TLV \_ 信标 \_ 探测 \_ 响应**](wdi-tlv-beacon-probe-response.md)                 |                                | X        | 端口接收到的最新信标或探测响应帧。 这不包括 802.11 MAC 标头。                                                                                                |
| [**WDI \_ TLV \_ ETHERTYPE \_ ENCAP \_ 表**](wdi-tlv-ethertype-encap-table.md)                 |                                | X        | 关联的 Ethertype 封装。                                                                                                                                                           |
| [**WDI \_ TLV \_ PHY \_ 类型 \_ 列表**](wdi-tlv-phy-type-list.md)                                 |                                | X        | 在 BSS 网络连接上，802.11 工作站用于发送或接收数据包的 PHY 标识符的列表。                                                                                          |

 

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

 

 




