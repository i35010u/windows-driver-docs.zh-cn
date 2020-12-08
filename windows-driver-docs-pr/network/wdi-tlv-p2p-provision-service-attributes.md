---
title: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES
description: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES 是包含 Wi-Fi 直接预配服务属性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2ec74a4839d4da1f17dda293de67c6af9b9a616e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818199"
---
# <a name="wdi_tlv_p2p_provision_service_attributes"></a>WDI \_ TLV \_ P2P \_ 预配 \_ 服务 \_ 属性


WDI \_ tlv \_ P2P \_ 预配 \_ 服务 \_ 属性是一个 Tlv，其中包含 Wi-Fi 直接预配服务属性。

## <a name="tlv-type"></a>TLV 类型


0xC6

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-Fi 直接状态代码，如 Wi-Fi 直接规范所定义。                                                                            |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 用于未来 Wi-Fi 直接连接的本地 MAC 地址。                                                                                              |
| UINT8                                             | 连接功能位掩码。                                                                                                                     |
| UINT32                                            | 功能功能位掩码。                                                                                                                        |
| UINT32                                            | 服务实例的播发 ID。                                                                                                         |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 服务实例的服务地址。                                                                                                          |
| UINT32                                            | 唯一标识服务会话的会话 ID。                                                                                    |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 唯一标识服务会话的会话地址。                                                                               |
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

 

