---
title: OID_WDI_SET_ENCAPSULATION_OFFLOAD
description: OS 发送 OID_WDI_SET_ENCAPSULATION_OFFLOAD 以指示较低边缘驱动程序 (LE) 应开始这样做 TCP 校验和/LSO 将卸载。
ms.assetid: 1095DBE0-2C6B-40F4-8E01-39F4BBA2FDBC
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ENCAPSULATION_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c3bf12d25f2862372127cd8e3d2316e948d64a20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354498"
---
# <a name="oidwdisetencapsulationoffload"></a>OID\_WDI\_SET\_ENCAPSULATION\_OFFLOAD


OID\_WDI\_设置\_封装\_卸载发送由操作系统，以指示较低边缘驱动程序 (LE) 应开始执行 TCP 校验和/LSO 卸载。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 是                      | 1                               |

 

LE 收到此消息后，应指示其当前的封装卸载配置与[NDIS\_状态\_WDI\_指示\_任务\_卸载\_当前\_配置](ndis-status-wdi-indication-task-offload-current-config.md)。 对于接收操作，LE 应启动直到校验和卸载后收到 OID\_WDI\_设置\_封装\_卸载消息。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                                                   | 允许多个 TLV 实例 | 可选 | 描述                                     |
|-----------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_SET\_ENCAPSULATION\_OFFLOAD\_V4\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-encapsulation-offload-v4-parameters) |                                |          | 指定是否应启动 IPv4 卸载。 |
| [**WDI\_TLV\_SET\_ENCAPSULATION\_OFFLOAD\_V6\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-set-encapsulation-offload-v6-parameters) |                                |          | 指定是否应启动 IPv6 卸载。 |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




