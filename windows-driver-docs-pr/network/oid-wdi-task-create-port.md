---
title: OID_WDI_TASK_CREATE_PORT
description: OID_WDI_TASK_CREATE_PORT 请求由 IHV 组件创建新的802.11 实体。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CREATE_PORT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 81d9ecdb96287b666c3f25f8d773ac659c8cb9c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829289"
---
# <a name="oid_wdi_task_create_port"></a>OID \_ WDI \_ 任务 \_ 创建 \_ 端口


OID \_ WDI \_ TASK \_ CREATE \_ PORT 请求由 IHV 组件创建新的802.11 实体。

| 对象  | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 6                                     | 1                               |

 

创建的端口的操作模式设置为 **WDI \_ 操作 \_ 模式 \_ STA** ，除非它已在任务参数中指定。

如果 MAC 充当 Wi-Fi Direct 设备端口， **uOpmodeMask** 将包含 **WDI \_ 操作 \_ 模式 \_ P2P \_ 设备**。 在这种情况下，IHV 组件驱动程序必须将为 Wi-Fi Direct 设备保留的 MAC 地址分配到此端口，并在请求完成指示中返回。

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-create-port-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_CREATE_PORT_PARAMETERS&lt;/strong&gt;](./wdi-tlv-create-port-parameters.md)"><strong>WDI_TLV_CREATE_PORT_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>用于创建端口的参数。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-create-port-mac-address" data-raw-source="[&lt;strong&gt;WDI_TLV_CREATE_PORT_MAC_ADDRESS&lt;/strong&gt;](./wdi-tlv-create-port-mac-address.md)"><strong>WDI_TLV_CREATE_PORT_MAC_ADDRESS</strong></a></td>
<td></td>
<td>X</td>
<td><p>当在从休眠状态恢复期间，UE 重新创建非主端口时，将使用此 TLV。 如果存在此 TLV，固件必须使用此 MAC 地址来创建端口。 此 MAC 地址保证是固件在休眠之前为端口类型创建的 MAC 地址。</p>
<p>目标是使用相同的 NDIS 端口号和 MAC 地址，以便与上层的状态相匹配。 请注意，WFC_PORT_ID 可以在重新使用时有所不同，但端口 ID 不应与现有端口的任何端口 ID 冲突。 此信息仅用于 UE 和 LE/固件之间。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 创建 \_ 端口 \_ 完成](ndis-status-wdi-indication-create-port-complete.md)

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

