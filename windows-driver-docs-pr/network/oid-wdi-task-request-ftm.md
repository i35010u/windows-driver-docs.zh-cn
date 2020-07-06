---
title: OID_WDI_TASK_REQUEST_FTM
description: 将 OID_WDI_TASK_REQUEST_FTM 颁发给 LE，以启动具有列出的 BSS 目标的精细计时度量（INTERNAL.H）过程。
ms.assetid: 67E17BD2-9216-43B5-8D1E-C6DF8537D79E
ms.date: 02/08/2019
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_REQUEST_FTM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a7e2cf3a171a59613e11575b7b6c2e9025620856
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968536"
---
# <a name="oid_wdi_task_request_ftm"></a>OID_WDI_TASK_REQUEST_FTM


将**OID_WDI_TASK_REQUEST_FTM**颁发给 LE，以启动具有列出的 BSS 目标的精细计时度量（internal.h）过程。 目标数小于或等于从工作站特性获取的**FTMNumberOfSupportedTargets**的值。

当目标的所有 INTERNAL.H 会话完成、超时已过期或主机已中止操作时，应立即完成此任务。

完成此任务后，驱动程序应发送一个[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)状态指示，其中包含每个请求的目标的 internal.h 响应列表。

完成此任务后，端口应处于良好状态并且应准备好处理新的 INTERNAL.H 请求，因为主机可能会立即使用一组新的目标重新尝试该任务。

对于每个目标，如果应请求位置配置信息（LCI）报告，则指示。 如果指示，则该 LE 应从目标请求一个。 

## <a name="task-parameters"></a>任务参数

| TLV | 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | UINT32 |   |   | 完成 INTERNAL.H 的最长时间（以毫秒为单位）。 超时值设置为150毫秒，乘以目标的数目。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | WDI_FTM_TARGET_BSS_ENTRY | X |   | 应完成其 INTERNAL.H 过程的 BSS 目标的列表。 |

## <a name="task-completion-indication"></a>任务完成指示

[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1903

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi

