---
title: WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY
description: WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY 为 TLV，其中包含 ASP2 服务信息发现条目。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b8ffa3e10a1395494716155e36ee4cb87146d111
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823775"
---
# <a name="wdi_tlv_p2p_asp2_service_information_discovery_entry"></a>WDI \_ TLV \_ P2P \_ ASP2 \_ 服务 \_ 信息 \_ 发现 \_ 条目


WDI \_ tlv \_ P2P \_ ASP2 \_ 服务 \_ 信息 \_ 发现 \_ 条目是包含 ASP2 服务信息发现条目的 tlv。

**注意**  此 TLV 已添加到 Windows 10 版本1607，WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12D

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                      | 允许多个 TLV 实例 | 可选 | 说明                                                                                                         |
|-------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称**](wdi-tlv-p2p-service-name.md)                          |                                |          | 服务名称 (UTF-8) ，最多21个字节。                                                                        |
| [**WDI \_ TLV \_ P2P \_ 实例 \_ 名称**](wdi-tlv-p2p-instance-name.md)                        |                                |          | 服务实例名称 (UTF-8) ，最大为63字节。                                                               |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 信息**](wdi-tlv-p2p-service-information.md)            |                                | X        | 请求服务信息将用于 ANQP 查询请求，以下载此服务的服务信息。 |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 更新 \_ 指示器**](wdi-tlv-p2p-service-update-indicator.md) |                                | X        | 要用于 ANQP 查询请求的服务更新指示器。                                                     |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 事务 \_ ID**](wdi-tlv-p2p-service-transaction-id.md)     |                                | X        | 要用于 ANQP 查询请求的服务事务 ID。                                                       |

 

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

 

 




