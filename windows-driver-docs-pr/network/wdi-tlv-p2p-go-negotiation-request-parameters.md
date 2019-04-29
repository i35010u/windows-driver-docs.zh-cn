---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS 是 TLV 包含 Wi-Fi Direct 组所有者协商请求参数。
ms.assetid: C0B1832A-D315-47F8-87B8-73373CF55D44
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 43f215cd6191ee1825615c6f111ae229c73d4621
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363643"
---
# <a name="wditlvp2pgonegotiationrequestparameters"></a>WDI\_TLV\_P2P\_GO\_NEGOTIATION\_REQUEST\_PARAMETERS


WDI\_TLV\_P2P\_转\_协商\_请求\_参数是包含 Wi-Fi Direct 组所有者协商请求参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x6E

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定本地 Wi-Fi Direct 转意向。 有效值介于 0 到 15 之间。                                                                                                  |
| UINT8                                             | 指定转意向的补救措施字段。                                                                                                                                   |
| UINT16                                            | 指定转配置超时以毫秒为单位。                                                                                                                         |
| UINT16                                            | 指定客户端配置超时以毫秒为单位。                                                                                                                     |
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 预期的接口地址。 指定供将来 Wi-Fi Direct 连接的本地 MAC 地址。                                                                                |
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

 

 




