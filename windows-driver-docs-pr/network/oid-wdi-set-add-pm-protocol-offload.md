---
title: OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD
description: OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD 为电源管理添加一个或多个协议卸载的列表。
ms.assetid: 50c69dd4-352d-484f-81c1-a4c9587ab368
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADD_PM_PROTOCOL_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1f66ebf037ba81c9680ae8faf4bf50acc241fe42
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215831"
---
# <a name="oid_wdi_set_add_pm_protocol_offload"></a>OID \_ WDI \_ 设置 \_ 添加 \_ PM \_ 协议 \_ 卸载


OID \_ WDI \_ SET \_ ADD \_ PM \_ 协议 \_ 卸载添加了一个或多个用于电源管理的协议卸载列表。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

此属性提供的信息使设备/固件能够在主 CPU 处于睡眠状态时实现这些协议。 在此状态下，固件和设备会在不唤醒主机的情况下处理已卸载的任务。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                            |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ IPv4ARP**](./wdi-tlv-pm-protocol-offload-ipv4arp.md)                |                                | X        | IPv4 ARP 协议卸载参数。  |
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ IPv6NS**](./wdi-tlv-pm-protocol-offload-ipv6ns.md)                  |                                | X        | IPv6 NS 协议卸载参数。   |
| [**WDI \_ TLV \_ PM \_ 协议 \_ 卸载 \_ 80211RSN \_ REKEY**](./wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) |                                | X        | RSN Rekey 协议卸载参数。 |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 获取 \_ PM \_ 协议 \_ 卸载](oid-wdi-get-pm-protocol-offload.md)

[OID \_ WDI \_ SET \_ 删除 \_ PM \_ 协议 \_ 卸载](oid-wdi-set-remove-pm-protocol-offload.md)

 

