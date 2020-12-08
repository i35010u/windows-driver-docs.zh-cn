---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO
description: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO 是包含 Wi-Fi 直接预配发现响应信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c783103b6b09e28430a17fc000d8cc27d93f260c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818195"
---
# <a name="wdi_tlv_p2p_provision_discovery_response_info"></a>WDI \_ TLV \_ P2P \_ 预配 \_ 发现 \_ 响应 \_ 信息


WDI \_ tlv \_ P2P \_ 预配 \_ 发现 \_ 响应信息 \_ 是一个 Tlv，其中包含 Wi-Fi 直接预配发现响应信息。

## <a name="tlv-type"></a>TLV 类型


0x87

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                                     | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 预配 \_ 发现 \_ 响应 \_ 参数**](wdi-tlv-p2p-provision-discovery-response-parameters.md) |                                |          | 预配发现响应参数。                                                                                                                                                                                            |
| [**WDI \_ TLV \_ P2P \_ 预配 \_ 服务 \_ 属性**](wdi-tlv-p2p-provision-service-attributes.md)                        |                                | X        | 设置服务属性。                                                                                                                                                                                                       |
| [**WDI \_ TLV \_ P2P \_ 组 \_ ID**](wdi-tlv-p2p-group-id.md)                                                                 |                                | X        | 如果支持 Wi-Fi Direct 服务，则为组 ID。                                                                                                                                                                                      |
| [**WDI \_ TLV \_ P2P \_ 永久性 \_ 组 \_ ID**](wdi-tlv-p2p-persistent-group-id.md)                                          |                                | X        | 用于连接的永久组的 IP 组。 如果 [**WDI \_ TLV \_ P2P \_ 预配 \_ 服务 \_ 属性**](wdi-tlv-p2p-provision-service-attributes.md) 中的永久组标志设置为1，则此字段有效。 |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 会话 \_ 信息**](wdi-tlv-p2p-service-session-info.md)                                        |                                | X        | 服务会话信息。                                                                                                                                                                                                        |

 

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

 

 




