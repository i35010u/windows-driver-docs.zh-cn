---
title: OID_WDI_SET_ADVERTISEMENT_INFORMATION
description: OID_WDI_SET_ADVERTISEMENT_INFORMATION 配置信息元素 (IEs) 和其他播发设置包含在探测请求、 探测响应，并由指定的端口发送的信号。
ms.assetid: efa1fc93-2cc8-4d14-be5f-d099ef3c371e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADVERTISEMENT_INFORMATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 234a9a733e924990ad39668c2ad04f434929d683
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365772"
---
# <a name="oidwdisetadvertisementinformation"></a>OID\_WDI\_设置\_播发\_信息


OID\_WDI\_设置\_播发\_信息将配置信息元素 (IEs) 和其他播发设置要包含在探测请求，探测响应，由发送信号指定的端口。 此请求操作仅适用于 Wi-Fi Direct 端口。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

当设备收到此命令时，它应更新任何相关 Wi-Fi Direct 导致浏览器，并追加任何必要其他导致浏览器在将来传出消息发送的此端口。

## <a name="set-property-parameters"></a>设置属性参数


WDI 可以播发服务提供一组预配置的前缀哈希。 如果对等方发送哈希，该驱动程序首先尝试与服务名称哈希匹配，如中所定义[ **WDI\_TLV\_P2P\_播发\_前缀\_条目**](https://msdn.microsoft.com/library/windows/hardware/mt269134). 如果从前缀哈希找到匹配项，该驱动程序将搜索中的服务[ **WDI\_TLV\_P2P\_播发\_服务\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn897861)的具有前缀和使用这些响应。 如果找不到匹配项，该驱动程序将尝试匹配请求的服务名称中的哈希[ **WDI\_TLV\_P2P\_播发\_服务\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn897861).

| TLV                                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                     |
|-----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_ADDITIONAL\_IES**](https://msdn.microsoft.com/library/windows/hardware/dn926122)                                    |                                | X        | 要包含的其他 IEs。                  |
| [**WDI\_TLV\_P2P\_DEVICE\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn897875)                                 |                                | X        | Wi-Fi Direct 设备信息。                |
| [**WDI\_TLV\_P2P\_DEVICE\_CAPABILITY**](https://msdn.microsoft.com/library/windows/hardware/dn897872)                     |                                | X        | Wi-Fi Direct 设备功能。               |
| [**WDI\_TLV\_P2P\_GROUP\_OWNER\_CAPABILITY**](https://msdn.microsoft.com/library/windows/hardware/dn897954)          |                                | X        | Wi-Fi Direct 组所有者功能信息 |
| [**WDI\_TLV\_P2P\_辅助\_设备\_类型\_列表**](https://msdn.microsoft.com/library/windows/hardware/dn897991) |                                | X        | Wi-Fi Direct 辅助设备类型的列表。    |
| [**WDI\_TLV\_P2P\_ADVERTISED\_SERVICES**](https://msdn.microsoft.com/library/windows/hardware/dn897860)                 |                                | X        | Wi-Fi Direct 播发服务。               |

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS\_状态\_WDI\_指示\_操作\_帧\_RECEIVED](ndis-status-wdi-indication-action-frame-received.md)适配器必须指示 ANQP 操作框架请求的服务信息如果它接收来自对等方 ANQP 请求 （或任何其他操作未知的帧）。

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

 

 




