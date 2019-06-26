---
title: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES
description: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES 是 TLV 包含 Wi-Fi Direct 预配服务属性。
ms.assetid: CA318E91-660A-4F17-827B-F27E18643CC6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5b498f207938e9640f6d107cede6c831e8f81511
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353296"
---
# <a name="wditlvp2pprovisionserviceattributes"></a>WDI\_TLV\_P2P\_PROVISION\_SERVICE\_ATTRIBUTES


WDI\_TLV\_P2P\_预配\_服务\_属性是包含 Wi-Fi Direct 预配服务特性 TLV。

## <a name="tlv-type"></a>TLV 类型


0xC6

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-Fi Direct 状态代码，如 Wi-Fi Direct 规范所定义。                                                                            |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 以后 Wi-Fi Direct 进行连接的本地 MAC 地址。                                                                                              |
| UINT8                                             | 连接功能位掩码。                                                                                                                     |
| UINT32                                            | 功能功能位掩码。                                                                                                                        |
| UINT32                                            | 服务实例的播发 ID。                                                                                                         |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 服务实例的服务地址。                                                                                                          |
| UINT32                                            | 唯一标识连接到该服务的会话的会话 ID。                                                                                    |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 唯一标识连接到该服务的会话的会话地址。                                                                               |
| UINT16                                            | 转配置超时以毫秒为单位。                                                                                                          |
| UINT16                                            | 客户端配置超时以毫秒为单位。                                                                                                      |
| UINT8                                             | 指示是否的永久组将用于连接的标志。 如果将使用的永久组，该标志设置为 1。                  |
| UINT8                                             | 指示此帧是否为后续的预配在发现的一部分的标志。 如果它是后续预配发现的一部分，该标志设置为 1。 |

 

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

 

 




