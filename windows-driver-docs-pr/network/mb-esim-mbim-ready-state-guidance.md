---
title: MB esim 卡 MBIM 就绪指南
description: MB esim 卡 MBIM 就绪指南
ms.assetid: E7EB5E6D-1858-4B94-AF91-05333CC93D8B
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a74ff0333adb8772a2b355e4c43819cf34ff738
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544299"
---
# <a name="mb-esim-mbim-ready-state-guidance"></a>MB esim 卡 MBIM 就绪指南

本主题针对 Windows 10 版本 1709年及更高版本上的 esim 卡方案上预期的 MBIM 就绪状态提供指南。 为正确的就绪状态符合可确保 OS 处理对这种情况下正常运行的所有更改。 

> [!IMPORTANT]
> 所有方案和本主题中的状态都假定 esim 卡支持卡映射到默认执行器、 执行器 0，且已通电。

| 方案 | MBIM_MS_UICCSLOT_STATE | MBIM_SUBSCRIBER_READY_STATE |
| --- | --- | --- |
| esim 卡具有仅 MF （无配置文件） | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNoEsimProfile |
| esim 卡与任何已启用配置文件 | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNoEsimProfile |
| esim 卡启用配置文件 | MBIMMsUICCSlotStateActiveEsim | MBIMSubscriberReadyStateInitialized |
| 在直通模式下的 esim 卡 | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNotInitialized |

当需要 MBIM_MS_UICCSLOT_STATE 和 MBIM_SUBSCRIBER_READY_STATE 了更改时，槽状态更改应有就绪状态更改。 

当启用新的配置文件或配置文件之间切换时，就绪状态应具有以下流：

![esim 卡 MBIM 就绪状态流切换配置文件时](images/esim_mbim_ready_state_flow.png "esim 卡 MBIM 就绪状态流切换配置文件时")

有关 MBIM_MS_UICCSLOT_STATE 详细信息，请参阅 MBIM_MS_UICCSLOT_STATE 表上[MB 多 SIM 操作 (MBIM_CID_MS_SLOT_INFO_STATUS)](mb-multi-sim-operations.md)。

有关 MBIM_SUBSCRIBER_READY_STATE 的详细信息，请参阅部分 10.5.2.3[公共标准，USB MBIM](https://go.microsoft.com/fwlink/p/?linkid=842064)。

