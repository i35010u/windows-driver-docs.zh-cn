---
title: OID_WDI_TASK_ROAM
description: OID_WDI_TASK_ROAM 适配器尝试从当前连接的 AP 漫游到新的 AP 的请求。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_ROAM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9c7c492537346cc866a58c31ecc2966f483ea47a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829237"
---
# <a name="oid_wdi_task_roam"></a>OID \_ WDI \_ 任务 \_ 漫游


OID \_ WDI \_ 任务 \_ 漫游请求适配器尝试从当前连接的 AP 漫游到新的 AP。

| 对象 | 支持中止                                                               | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|-----------------------------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是的。 如果在解除解除后中止，则必须后跟 dot11 reset。 | 4                                     | 10                              |

 

Microsoft 组件提供适配器应考虑漫游的首选 BSS 条目列表。

发出此命令时，如果其当前关联，适配器将需要与当前连接的 AP 解除关联，然后漫游到新的 AP。 在这种情况下，它首先指示旧 AP 的 "解除关联"，然后为新的 AP 指定关联结果，然后完成该任务。

它还可以确定不执行漫游并保持连接到当前 AP。 在这种情况下，它只会完成任务，无需任何关联或解除关联指示。

此任务的扫描和 AP 选择要求与 [OID \_ WDI \_ 任务 \_ 连接](oid-wdi-task-connect.md)的要求相同。

## <a name="task-parameters"></a>任务参数


| TLV  | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [**WDI \_ TLV \_ 连接 \_ 参数**](./wdi-tlv-connect-parameters.md) |   |   | 连接参数。 |  
| [**WDI \_ TLV \_ 连接 \_ BSS \_ 条目**](./wdi-tlv-connect-bss-entry.md)  | X  |   | 候选连接 BSS 条目的首选列表。 此端口应尝试连接到这些 BSS 条目，直到该列表已用尽或连接成功完成。 如果需要，此端口可以重新调整条目的优先级。 如果适配器设置了 "连接 BSS 选择替代位"，则它可以选择不在此列表中的 BSS，前提是它遵循允许/不允许列表要求。 | 

## <a name="task-completion-indication"></a>任务完成指示

[NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_ 完成](ndis-status-wdi-indication-roam-complete.md)

## <a name="unsolicited-indications"></a>未经请求的指示

[NDIS \_ 状态 \_ WDI \_ 指示 \_ 关联 \_ 结果](ndis-status-wdi-indication-association-result.md)

[NDIS \_ 状态 \_ WDI \_ 指示 \_ 解除了](ndis-status-wdi-indication-disassociation.md)

[NDIS \_ 状态 \_ WDI \_ 指示 \_ \_ 需要 FT ASSOC \_ 参数 \_](ndis-status-wdi-indication-ft-assoc-params-needed.md)

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

