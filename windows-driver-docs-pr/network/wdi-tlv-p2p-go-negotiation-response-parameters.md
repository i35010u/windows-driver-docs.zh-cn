---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS 是包含传入的中转协商响应参数的 TLV。
ms.assetid: 78C9B274-FAF0-4B2E-98A9-865A65105DA1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7a899d07fcc1dbb2ca017dfed89fb3c3609d2a59
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209573"
---
# <a name="wdi_tlv_p2p_go_negotiation_response_parameters"></a>WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 响应 \_ 参数


WDI \_ tlv \_ P2P \_ 中转 \_ 协商 \_ 响应 \_ 参数是包含传入的中转协商响应参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x71

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 按照 Wi-fi Direct 规范的定义，指定 Wi-fi Direct 状态代码。                                                                                           |
| UINT8                                             | 指定本地 Wi-fi Direct 中转意向。 这是一个介于0到15之间的值。                                                                                                   |
| UINT8                                             | 指定中转意向的 "断字符" 字段。                                                                                                                               |
| UINT16                                            | 指定中转配置超时值（以毫秒为单位）。                                                                                                                         |
| UINT16                                            | 指定客户端配置超时值（以毫秒为单位）。                                                                                                                     |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 预期接口地址。 指定用于未来 Wi-fi Direct 连接的本地 MAC 地址。                                                                                 |
| UINT8                                             | 指定 Wi-fi Direct Group 功能位掩码。 位掩码与 Wi-fi P2P 技术规范的表13组功能位图定义中定义的位掩码匹配。 |
| UINT8                                             | 指定操作系统在上述组功能位图中设置的位。                                                                                            |

 

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

 

