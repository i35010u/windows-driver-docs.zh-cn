---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_INFO
description: WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_INFO 是 TLV 包含 Wi-Fi Direct 预配发现请求的信息。
ms.assetid: C71F2FA9-2255-45E9-83CD-FA8DBEF5EA74
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cac289c152243e71c6ab03c98518bdfd88eb763a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362813"
---
# <a name="wditlvp2pprovisiondiscoveryrequestinfo"></a>WDI\_TLV\_P2P\_预配\_发现\_请求\_信息


WDI\_TLV\_P2P\_预配\_发现\_请求\_信息是 TLV 包含 Wi-Fi Direct 预配发现请求的信息。

## <a name="tlv-type"></a>TLV 类型


0x83

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                                   | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_预配\_发现\_请求\_参数**](wdi-tlv-p2p-provision-discovery-request-parameters.md) |                                |          | Wi-Fi Direct 预配发现请求的参数。                                                                                                                                                                                |
| [**WDI\_TLV\_P2P\_GROUP\_ID**](wdi-tlv-p2p-group-id.md)                                                               |                                | X        | Wi-Fi Direct 转的目标组 ID。 组 ID 是可选的。 如果是 Wi-Fi Direct 服务，这是本地 Wi-Fi Direct 转的远程端应加入的组 ID。                                       |
| [**WDI\_TLV\_P2P\_PROVISION\_SERVICE\_ATTRIBUTES**](wdi-tlv-p2p-provision-service-attributes.md)                      |                                | X        | Wi-Fi Direct 预配服务的属性。                                                                                                                                                                                          |
| [**WDI\_TLV\_P2P\_PERSISTENT\_GROUP\_ID**](wdi-tlv-p2p-persistent-group-id.md)                                        |                                | X        | 要用于连接的永久组组 IP。 此字段是有效的永久组标志中[ **WDI\_TLV\_P2P\_预配\_服务\_属性**](wdi-tlv-p2p-provision-service-attributes.md)设置为 1。 |
| [**WDI\_TLV\_P2P\_SERVICE\_SESSION\_INFO**](wdi-tlv-p2p-service-session-info.md)                                      |                                | X        | 服务会话的信息。 此字段无效，如果[ **WDI\_TLV\_P2P\_预配\_服务\_属性**](wdi-tlv-p2p-provision-service-attributes.md)存在。                                                                       |

 

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

 

 




