---
title: MB eSIM MBIM 就绪状态指导
description: MB eSIM MBIM 就绪状态指导
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f78040dc4f6e5d1e7c7bd1e0d3bf1b3d883f04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838421"
---
# <a name="mb-esim-mbim-ready-state-guidance"></a>MB eSIM MBIM 就绪状态指导

本主题提供有关 Windows 10 版本1709及更高版本上的 eSIM 方案的预期 MBIM 就绪状态的指导。 与正确的就绪状态一致，可确保操作系统为该方案正确处理所有更改。 

> [!IMPORTANT]
> 本主题中的所有方案和状态都假设已将 eSIM 功能的卡映射到默认执行器、执行器0，并且已打开。

| 方案 | MBIM_MS_UICCSLOT_STATE | MBIM_SUBSCRIBER_READY_STATE |
| --- | --- | --- |
| eSIM 仅限 MF (没有配置文件)  | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNoEsimProfile |
| eSIM，无启用配置文件 | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNoEsimProfile |
| 已启用配置文件的 eSIM | MBIMMsUICCSlotStateActiveEsim | MBIMSubscriberReadyStateInitialized |
| 在直通模式下 eSIM | MBIMMsUICCSlotStateActiveEsimNoProfiles | MBIMSubscriberReadyStateNotInitialized |

当需要更改 MBIM_MS_UICCSLOT_STATE 和 MBIM_SUBSCRIBER_READY_STATE 时，槽状态更改应在就绪状态更改之前。 

启用新的配置文件或在配置文件之间切换时，就绪状态应具有以下流：

![切换配置文件时的 eSIM MBIM 就绪状态流](images/esim_mbim_ready_state_flow.png "切换配置文件时的 eSIM MBIM 就绪状态流")

有关 MBIM_MS_UICCSLOT_STATE 的详细信息，请参阅用于 [MB 多 SIM 操作的 MBIM_MS_UICCSLOT_STATE 表 (MBIM_CID_MS_SLOT_INFO_STATUS) ](mb-multi-sim-operations.md)。

有关 MBIM_SUBSCRIBER_READY_STATE 的详细信息，请参阅 [公共 USB MBIM standard](https://www.usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement)的10.5.2.3 部分。

