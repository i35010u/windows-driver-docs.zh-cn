---
title: OID_WDI_SET_ADVERTISEMENT_INFORMATION
description: OID_WDI_SET_ADVERTISEMENT_INFORMATION 将信息元素 () 和其他要包含在探测请求中的播发设置、探测响应和由指定端口发送的信标配置。
ms.assetid: efa1fc93-2cc8-4d14-be5f-d099ef3c371e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADVERTISEMENT_INFORMATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 632c39fb881baf0c0bff2a9d3f0fc3c91a90266d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213269"
---
# <a name="oid_wdi_set_advertisement_information"></a>OID \_ WDI \_ 设置 \_ 播发 \_ 信息


OID \_ WDI \_ SET \_ 播发 \_ 信息将 (的信息元素配置为在探测请求、探测响应和由指定端口发送的信标中包含的) 和其他播发设置。 此请求仅适用于 Wi-fi 直接端口。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

当设备收到此命令时，它应更新任何相关的 Wi-fi Direct，并在将来发送此端口发送的传出消息中附加任何必要的附加项。

## <a name="set-property-parameters"></a>设置属性参数


WDI 可以为播发服务提供一组预配置的前缀哈希。 如果对等方发送哈希，则驱动程序将首先尝试与 [**WDI \_ TLV \_ P2P \_ 播发 \_ 前缀 \_ 条目**](./wdi-tlv-p2p-advertised-prefix-entry.md)中定义的服务名称哈希匹配。 如果从前缀哈希中找到匹配项，则驱动程序会在具有前缀的 [**WDI \_ TLV \_ P2P \_ 播发 \_ 服务 \_ 项**](./wdi-tlv-p2p-advertised-service-entry.md) 中搜索服务 () ，并使用这些内容做出响应。 如果找不到匹配项，驱动程序将尝试与 [**WDI \_ TLV \_ P2P \_ 播发 \_ 服务 \_ 项**](./wdi-tlv-p2p-advertised-service-entry.md)中请求的服务名称哈希匹配。

| TLV                                                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                     |
|-----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI \_ TLV \_ 补充 \_**](./wdi-tlv-additional-ies.md)                                    |                                | X        | 要包括的其他补充。                  |
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 信息**](./wdi-tlv-p2p-device-info.md)                                 |                                | X        | Wi-fi Direct 设备信息。                |
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 功能**](./wdi-tlv-p2p-device-capability.md)                     |                                | X        | Wi-fi Direct 设备功能。               |
| [**WDI \_ TLV \_ P2P \_ 组 \_ 所有者 \_ 功能**](./wdi-tlv-p2p-group-owner-capability.md)          |                                | X        | Wi-fi Direct 组所有者功能信息 |
| [**WDI \_ TLV \_ P2P \_ 辅助 \_ 设备 \_ 类型 \_ 列表**](./wdi-tlv-p2p-secondary-device-type-list.md) |                                | X        | Wi-fi Direct 辅助设备类型的列表。    |
| [**WDI \_ TLV \_ P2P \_ 播发 \_ 服务**](./wdi-tlv-p2p-advertised-services.md)                 |                                | X        | Wi-fi Direct 播发服务。               |

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS \_状态 \_ WDI \_ 指示 \_ 操作 \_ 帧 \_ 收到](ndis-status-wdi-indication-action-frame-received.md) 的适配器必须指示服务信息的 ANQP 操作帧请求，以获取对等方) 的 ANQP 请求 (或任何其他未知操作帧。

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

 

