---
title: WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY
description: WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY 是包含 ASP2 服务信息发现条目 TLV。
ms.assetid: 67F1CDE2-8003-44D3-B338-FE7C5EA48C29
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b33c81a656e84895a10024b79a393cbac6d299ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365728"
---
# <a name="wditlvp2pasp2serviceinformationdiscoveryentry"></a>WDI\_TLV\_P2P\_ASP2\_服务\_信息\_发现\_条目


WDI\_TLV\_P2P\_ASP2\_服务\_信息\_发现\_项是包含 ASP2 服务信息发现条目 TLV。

**请注意**  此 TLV 添加 Windows 10，版本 1607，WDI 版本 1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12D

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                                                         |
|-------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_SERVICE\_NAME**](wdi-tlv-p2p-service-name.md)                          |                                |          | 服务 (utf-8)，最多 21 字节的名称。                                                                        |
| [**WDI\_TLV\_P2P\_INSTANCE\_NAME**](wdi-tlv-p2p-instance-name.md)                        |                                |          | 实例最多 63 个字节 (UTF-8) 的服务的名称。                                                               |
| [**WDI\_TLV\_P2P\_服务\_信息**](wdi-tlv-p2p-service-information.md)            |                                | X        | 要用于 ANQP 查询请求以下载此服务的服务信息的请求服务信息。 |
| [**WDI\_TLV\_P2P\_SERVICE\_UPDATE\_INDICATOR**](wdi-tlv-p2p-service-update-indicator.md) |                                | X        | 要用于 ANQP 查询请求的服务更新指示器。                                                     |
| [**WDI\_TLV\_P2P\_SERVICE\_TRANSACTION\_ID**](wdi-tlv-p2p-service-transaction-id.md)     |                                | X        | 要用于 ANQP 查询请求的服务事务 ID。                                                       |

 

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

 

 




