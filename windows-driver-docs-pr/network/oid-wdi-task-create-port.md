---
title: OID_WDI_TASK_CREATE_PORT
description: OID_WDI_TASK_CREATE_PORT 请求，IHV 组件，创建新的 802.11 实体。
ms.assetid: e1a03a97-608f-42af-bd39-37a7eb9ad5b7
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CREATE_PORT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c218861294d13130d5529d9c60c55e122102ab84
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59904001"
---
# <a name="oidwditaskcreateport"></a>OID\_WDI\_TASK\_CREATE\_PORT


OID\_WDI\_任务\_创建\_端口请求，IHV 组件，创建新的 802.11 实体。

| Object  | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 6                                     | 1                               |

 

创建端口的操作模式设置为**WDI\_操作\_模式\_STA**除非任务参数中指定了。

如果将函数作为 Wi-Fi Direct 设备端口，MAC **uOpmodeMask**包含**WDI\_操作\_模式\_P2P\_设备**。 在这种情况下，IHV 组件驱动程序必须将保留的 MAC 地址分配到此端口 Wi-Fi Direct 设备并将其返回在请求完成指示。

## <a name="task-parameters"></a>任务参数


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926273" data-raw-source="[&lt;strong&gt;WDI_TLV_CREATE_PORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926273)"><strong>WDI_TLV_CREATE_PORT_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>用于端口创建的参数。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926270" data-raw-source="[&lt;strong&gt;WDI_TLV_CREATE_PORT_MAC_ADDRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926270)"><strong>WDI_TLV_CREATE_PORT_MAC_ADDRESS</strong></a></td>
<td></td>
<td>X</td>
<td><p>此 TLV UE 从休眠状态恢复运行时将重新创建非主端口时使用。 如果存在此 TLV，则固件必须使用此 MAC 地址创建端口。 要为之前休眠状态，端口类型创建固件的 MAC 地址，保证此 MAC 地址。</p>
<p>目标是使用相同的 NDIS 端口号和 MAC 地址来匹配上层的状态。 请注意，WFC_PORT_ID 可以是不同，重新创建，但端口 ID 应不会使用现有端口的任何端口 ID 冲突。 UE 和 LE/固件之间仅使用此信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_创建\_端口\_完成](ndis-status-wdi-indication-create-port-complete.md)

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

 

 




