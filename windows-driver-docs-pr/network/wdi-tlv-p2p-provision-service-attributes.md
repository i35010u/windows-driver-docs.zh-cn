---
title: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES
description: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES 是包含 Wi-fi Direct 预配服务属性的 TLV。
ms.assetid: CA318E91-660A-4F17-827B-F27E18643CC6
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 90098dd89339c0c3820efb4258c8af563410c3b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845128"
---
# <a name="wdi_tlv_p2p_provision_service_attributes"></a>WDI\_TLV\_P2P\_预配\_服务\_属性


WDI\_TLV\_P2P\_预配\_服务\_属性是包含 Wi-fi Direct 预配服务属性的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xC6

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-fi Direct 状态代码，由 Wi-fi Direct 规范定义。                                                                            |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 用于未来 Wi-fi Direct 连接的本地 MAC 地址。                                                                                              |
| UINT8                                             | 连接功能位掩码。                                                                                                                     |
| UINT32                                            | 功能功能位掩码。                                                                                                                        |
| UINT32                                            | 服务实例的播发 ID。                                                                                                         |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 服务实例的服务地址。                                                                                                          |
| UINT32                                            | 唯一标识服务会话的会话 ID。                                                                                    |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 唯一标识服务会话的会话地址。                                                                               |
| UINT16                                            | 中转配置超时（毫秒）。                                                                                                          |
| UINT16                                            | 客户端配置超时（毫秒）。                                                                                                      |
| UINT8                                             | 一个标志，用于指示是否将永久组用于连接。 如果将使用永久性组，则将标志设置为1。                  |
| UINT8                                             | 一个标志，用于指示此框架是否是跟踪预配发现的一部分。 如果该标志是跟进预配发现的一部分，则该标志设置为1。 |

 

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

 

 




