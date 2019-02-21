---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO
description: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO 是 TLV 包含 Wi-Fi Direct 预配发现响应信息。
ms.assetid: EB7C4A5C-27D8-4A84-BC91-0DED51FB74C2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b050269fe829f12a5db03f6576015983316ea334
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520057"
---
# <a name="wditlvp2pprovisiondiscoveryresponseinfo"></a>WDI\_TLV\_P2P\_预配\_发现\_响应\_信息


WDI\_TLV\_P2P\_预配\_发现\_响应\_信息是包含 Wi-Fi Direct 配置发现响应信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x87

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                                     | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_预配\_发现\_响应\_参数**](wdi-tlv-p2p-provision-discovery-response-parameters.md) |                                |          | 预配发现响应参数。                                                                                                                                                                                            |
| [**WDI\_TLV\_P2P\_PROVISION\_SERVICE\_ATTRIBUTES**](wdi-tlv-p2p-provision-service-attributes.md)                        |                                | X        | 预配服务属性中。                                                                                                                                                                                                       |
| [**WDI\_TLV\_P2P\_GROUP\_ID**](wdi-tlv-p2p-group-id.md)                                                                 |                                | X        | 如果支持 Wi-Fi Direct 服务组的 ID。                                                                                                                                                                                      |
| [**WDI\_TLV\_P2P\_PERSISTENT\_GROUP\_ID**](wdi-tlv-p2p-persistent-group-id.md)                                          |                                | X        | 要用于连接的永久组组 IP。 此字段是有效的永久组标志中[ **WDI\_TLV\_P2P\_预配\_服务\_属性**](wdi-tlv-p2p-provision-service-attributes.md)设置为 1。 |
| [**WDI\_TLV\_P2P\_SERVICE\_SESSION\_INFO**](wdi-tlv-p2p-service-session-info.md)                                        |                                | X        | 服务会话的信息。                                                                                                                                                                                                        |

 

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

 

 




