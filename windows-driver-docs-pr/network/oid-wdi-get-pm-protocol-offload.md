---
title: OID_WDI_GET_PM_PROTOCOL_OFFLOAD
description: OID_WDI_GET_PM_PROTOCOL_OFFLOAD 请求电源管理的协议卸载列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_PM_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71475e6f2a041840d27b189863ad9c8d8f178da5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828451"
---
# <a name="oid_wdi_get_pm_protocol_offload"></a>OID \_ WDI \_ 获取 \_ PM \_ 协议 \_ 卸载


OID \_ WDI \_ 获取 \_ PM \_ 协议 \_ 卸载请求电源管理的协议卸载列表。

| 范围 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 不适用           | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


| TLV                                                                                  | 允许多个 TLV 实例 | 可选 | 说明          |
|--------------------------------------------------------------------------------------|--------------------------------|----------|----------------------|
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ GET**](./wdi-tlv-pm-protocol-offload-get.md) |                                |          | 协议卸载 ID。 |

 

## <a name="get-property-results"></a>获取属性结果


| TLV                                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ IPv4ARP**](./wdi-tlv-pm-protocol-offload-ipv4arp.md)                |                                | X        | IPv4 ARP 协议卸载参数。  |
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ IPv6NS**](./wdi-tlv-pm-protocol-offload-ipv6ns.md)                  |                                | X        | IPv6 NS 协议卸载参数。   |
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ 80211RSN \_ REKEY**](./wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) |                                | X        | RSN Rekey 协议卸载参数。 |

 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 设置 \_ 添加 \_ PM \_ 协议 \_ 卸载](oid-wdi-set-add-pm-protocol-offload.md)

[OID \_ WDI \_ SET \_ 删除 \_ PM \_ 协议 \_ 卸载](oid-wdi-set-remove-pm-protocol-offload.md)

 

