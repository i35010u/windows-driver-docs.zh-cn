---
title: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS
description: OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 是发送到设备与操作系统设置 TCP 卸载参数。
ms.assetid: B615066B-3871-4445-8397-B41CB66EEF35
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 586ca294c072473e3fb62e85829e19893999f985
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348511"
---
# <a name="oidwdisettcpoffloadparameters"></a>OID\_WDI\_SET\_TCP\_OFFLOAD\_PARAMETERS


OID\_WDI\_设置\_TCP\_卸载\_参数发送给该设备与操作系统设置 TCP 卸载参数。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

发送此命令在某些情况下，例如时则需要关闭由于性能问题而卸载。

较低边缘驱动程序 (LE) 必须使用的内容[ **WDI\_TLV\_TCP\_设置\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn898071)更新当前报告 TCP 卸载功能。 更新后，LE 必须报告的当前任务卸载能力[NDIS\_状态\_WDI\_指示\_任务\_卸载\_当前\_配置](ndis-status-wdi-indication-task-offload-current-config.md)。 此状态指示可确保所有基础协议驱动程序使用新的功能信息更新。

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                           |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI\_TLV\_TCP\_SET\_OFFLOAD\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn898071) |                                |          | TCP 卸载设置参数。 |

 

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

 

 




