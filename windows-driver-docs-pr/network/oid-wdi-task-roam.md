---
title: OID_WDI_TASK_ROAM
description: 适配器尝试从当前连接的 AP 漫游到一个新的 OID_WDI_TASK_ROAM 请求。
ms.assetid: 22976d21-9212-4915-ab7a-fcc15d228db1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_ROAM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e72a78d92e4bece93c9ad26a7287667c4c13d27a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387230"
---
# <a name="oidwditaskroam"></a>OID\_WDI\_TASK\_ROAM


OID\_WDI\_任务\_漫游适配器尝试从当前连接的 AP 漫游到一个新的请求。

| Object | 中止支持                                                               | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|-----------------------------------------------------------------------------|---------------------------------------|---------------------------------|
| Port   | 是。 如果中止在解除关联后，它必须后接 dot11 重置。 | 4                                     | 10                              |

 

Microsoft 组件提供适配器应考虑为漫游的首选 BSS 项的列表。

发出此命令后，如果其当前关联，适配器需要从当前连接的 AP 取消关联，然后漫游到新的应用程序。 在这种情况下它将首先指示解除关联的旧的 AP，则指示关联结果的新应用程序，然后完成任务。

它还可以确定无法执行漫游和保持连接到当前接入点。 在这种情况下它将仅完成任务，而无需任何关联或解除关联的指示。

扫描和亚太选择要求为此任务是同样适用于[OID\_WDI\_任务\_CONNECT](oid-wdi-task-connect.md)。

## <a name="task-parameters"></a>任务参数


| TLV  | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_CONNECT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-parameters) |   |   | 连接参数。 |  
| [**WDI\_TLV\_CONNECT\_BSS\_条目**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-bss-entry)  | X  |   | 首选的候选项列表连接 BSS 条目。 端口应尝试连接到这些 BSS 条目，直到耗尽列表或已成功完成的连接。 如果需要该端口可以重新调整条目。 如果适配器设置连接 BSS 选择重写位，它可以选择不在此列表中，只要它遵循的允许/不允许列表要求 BSS。 | 

## <a name="task-completion-indication"></a>指示任务完成

[NDIS\_状态\_WDI\_指示\_漫游\_完成](ndis-status-wdi-indication-roam-complete.md)

## <a name="unsolicited-indications"></a>未经请求的迹象

[NDIS\_状态\_WDI\_指示\_关联\_结果](ndis-status-wdi-indication-association-result.md)

[NDIS\_状态\_WDI\_指示\_解除关联](ndis-status-wdi-indication-disassociation.md)

[NDIS\_状态\_WDI\_指示\_FT\_ASSOC\_PARAMS\_需执行](ndis-status-wdi-indication-ft-assoc-params-needed.md)

[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)

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

 

 




