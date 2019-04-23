---
title: OID_WDI_TASK_REQUEST_FTM
description: OID_WDI_TASK_REQUEST_FTM 颁发给 LE 启动使用列出的 BSS 目标的正常时间度量 (FTM) 过程。
ms.assetid: 67E17BD2-9216-43B5-8D1E-C6DF8537D79E
ms.date: 02/08/2019
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_REQUEST_FTM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e4d4a295aaa71d6bd80ab3dcbcf371ec77809cc8
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905228"
---
# <a name="oidwditaskrequestftm"></a>OID_WDI_TASK_REQUEST_FTM


**OID_WDI_TASK_REQUEST_FTM**颁发给 LE 启动使用列出的 BSS 目标的正常时间度量 (FTM) 过程。 目标数小于或等于的值**FTMNumberOfSupportedTargets**，从工作站属性获得。

一旦完成目标的所有 FTM 会话、 超时已过期，或该主机已中止该操作，应都完成此任务。

完成此任务后，驱动程序应发送[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md) FTM 响应的列表包含为每个请求的目标的状态指示。

完成此任务后，该端口应处于良好状态，并应该已准备好处理新的 FTM 请求，因为主机立即重新尝试该任务的一组新的目标。

对于每个目标，指示如果应请求位置配置信息 (LCI) 报表。 如果已指明，LE 应请求来自目标。 

## <a name="task-parameters"></a>任务参数

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | UINT32 |   |   | 最长的时间，以毫秒为单位，以完成 FTM。 超时设置为 150 毫秒的目标数的乘积。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | WDI_FTM_TARGET_BSS_ENTRY | X |   | 应使用哪个 FTM 完成过程的 BSS 目标的列表。 |

## <a name="task-completion-indication"></a>指示任务完成

[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |
