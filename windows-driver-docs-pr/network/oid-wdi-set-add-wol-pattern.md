---
title: OID_WDI_SET_ADD_WOL_PATTERN
description: OID_WDI_SET_ADD_WOL_PATTERN 将 LAN 唤醒 (WOL) 模式添加到固件。
ms.assetid: 96fb71fd-412b-4013-b3bc-c31a43516f55
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADD_WOL_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0c7f35e6fe6eae02a539810ae7f1e0d7918d044a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215841"
---
# <a name="oid_wdi_set_add_wol_pattern"></a>OID \_ WDI \_ 设置 \_ 添加 \_ WOL \_ 模式


OID \_ WDI \_ SET \_ 添加 \_ WOL \_ 模式向固件添加 LAN 唤醒 (WOL) 模式。

| 作用域 | 设置序列化任务 | 正常执行时间 (秒)  |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

主机定义要添加到固件的数据包模式类型。 该固件检测到以 Dx 表示的匹配数据包。 如果检测到此情况，固件将断言唤醒中断。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                              | 允许多个 TLV 实例 | 可选 | 说明                                   |
|------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI \_ TLV \_ 唤醒 \_ 数据包 \_ 位图 \_ 模式**](./wdi-tlv-wake-packet-bitmap-pattern.md)                       | X                              | X        | WOL 模式信息。                      |
| [**WDI \_ TLV \_ 唤醒 \_ 数据包 \_ 幻 \_ 数据包**](./wdi-tlv-wake-packet-magic-packet.md)                           |                                | X        | 幻数据包的模式 ID。               |
| [**WDI \_ TLV \_ 唤醒 \_ 数据包 \_ IPv4 \_ TCP \_ 同步**](./wdi-tlv-wake-packet-ipv4-tcp-sync.md)                        | X                              | X        | WOL IPv4 TCP 同步数据包信息。         |
| [**WDI \_ TLV \_ 唤醒 \_ 数据包 \_ IPv6 \_ TCP \_ 同步**](./wdi-tlv-wake-packet-ipv6-tcp-sync.md)                        | X                              | X        | WOL IPv4 TCP 同步数据包信息。         |
| [**WDI \_ TLV \_ 唤醒 \_ 数据包 \_ EAPOL \_ 请求 \_ ID \_ 消息**](./wdi-tlv-wake-packet-eapol-request-id-message.md) |                                | X        | EAPOL 请求 ID 消息的 WOL 模式 ID。 |

 

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


[OID \_ WDI \_ SET \_ 删除 \_ WOL \_ 模式](oid-wdi-set-remove-wol-pattern.md)

 

