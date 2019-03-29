---
title: WDI_TLV_ASSOCIATION_RESULT
description: WDI_TLV_ASSOCIATION_RESULT 是 TLV，其中包含关联的结果。
ms.assetid: E0059A7A-0D20-403E-9A46-9633396A87C4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESULT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d556abb4211f97a067c2013035cddbd46df70d9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568176"
---
# <a name="wditlvassociationresult"></a>WDI\_TLV\_关联\_结果


WDI\_TLV\_关联\_结果是包含结果的关联 TLV。

## <a name="tlv-type"></a>TLV 类型


0x35

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                       | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                 |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSSID**](wdi-tlv-bssid.md)                                                   |                                |          | BSS BSSID。                                                                                                                                                                                       |
| [**WDI\_TLV\_关联\_结果\_参数**](wdi-tlv-association-result-parameters.md) |                                |          | 关联结果参数。                                                                                                                                                                          |
| [**WDI\_TLV\_ASSOCIATION\_REQUEST\_FRAME**](wdi-tlv-association-request-frame.md)         |                                | X        | 关联请求所用的关联。 这不包括 802.11 MAC 报头。                                                                                                         |
| [**WDI\_TLV\_关联\_响应\_帧**](wdi-tlv-association-response-frame.md)       |                                | X        | 收到关联响应。 这不包括 802.11 MAC 报头。                                                                                                                    |
| [**WDI\_TLV\_身份验证\_响应\_帧**](wdi-tlv-authentication-response-frame.md) |                                | X        | 失败代码收到身份验证响应。 这不包括 802.11 MAC 报头。 如果连接尝试失败，在身份验证交换期间，它应只能包含。 |
| [**WDI\_TLV\_信号\_探测\_响应**](wdi-tlv-beacon-probe-response.md)                 |                                | X        | 最新信号或探测端口接收的响应帧。 这不包括 802.11 MAC 报头。                                                                                                |
| [**WDI\_TLV\_ETHERTYPE\_ENCAP\_TABLE**](wdi-tlv-ethertype-encap-table.md)                 |                                | X        | 关联 Ethertype 封装。                                                                                                                                                           |
| [**WDI\_TLV\_PHY\_TYPE\_LIST**](wdi-tlv-phy-type-list.md)                                 |                                | X        | 802.11 工作站使用来发送或接收数据包的 BSS 网络连接上的物理标识符的列表。                                                                                          |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




