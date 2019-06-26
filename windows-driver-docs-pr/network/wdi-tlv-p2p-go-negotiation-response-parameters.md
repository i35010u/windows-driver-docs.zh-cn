---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS 是 TLV 包含传入转协商响应参数。
ms.assetid: 78C9B274-FAF0-4B2E-98A9-865A65105DA1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 24937e49bcddc8d744ff3a2a4dca2a9d71e5f5b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374696"
---
# <a name="wditlvp2pgonegotiationresponseparameters"></a>WDI\_TLV\_P2P\_转\_协商\_响应\_参数


WDI\_TLV\_P2P\_转\_协商\_响应\_参数是包含传入转协商响应参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x71

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定 Wi-Fi Direct 状态代码，如 Wi-Fi Direct 规范所定义。                                                                                           |
| UINT8                                             | 指定本地 Wi-Fi Direct 转意向。 这是介于 0 到 15 之间的值。                                                                                                   |
| UINT8                                             | 指定转意向的补救措施字段。                                                                                                                               |
| UINT16                                            | 指定转配置超时以毫秒为单位。                                                                                                                         |
| UINT16                                            | 指定客户端配置超时以毫秒为单位。                                                                                                                     |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 预期的接口地址。 指定未来 Wi-Fi Direct 连接的本地 MAC 地址。                                                                                 |
| UINT8                                             | 指定 Wi-Fi Direct 组功能位掩码。 位掩码相匹配的 Wi-fi P2P 技术规范的表 13 组功能位图定义中定义。 |
| UINT8                                             | 指定上述组功能位图中的操作系统设置的位。                                                                                            |

 

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

 

 




