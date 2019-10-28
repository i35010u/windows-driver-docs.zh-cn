---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS 是包含 Wi-fi Direct 组所有者协商请求参数的 TLV。
ms.assetid: C0B1832A-D315-47F8-87B8-73373CF55D44
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0af7172f4818fbadf945f527c11f8ca9bc6552eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840444"
---
# <a name="wdi_tlv_p2p_go_negotiation_request_parameters"></a>WDI\_TLV\_P2P\_中转\_协商\_请求\_参数


WDI\_TLV\_P2P\_中转\_协商\_请求\_参数是包含 Wi-fi Direct 组所有者协商请求参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x6E

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定本地 Wi-fi Direct 中转意向。 有效值介于0到15之间。                                                                                                  |
| UINT8                                             | 指定 "前往意向" 的 "断字符" 字段。                                                                                                                                   |
| UINT16                                            | 指定中转配置超时值（以毫秒为单位）。                                                                                                                         |
| UINT16                                            | 指定客户端配置超时值（以毫秒为单位）。                                                                                                                     |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 预期接口地址。 指定用于未来 Wi-fi Direct 连接的本地 MAC 地址。                                                                                |
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
<td><p>Windows 10</p></td>
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

 

 




