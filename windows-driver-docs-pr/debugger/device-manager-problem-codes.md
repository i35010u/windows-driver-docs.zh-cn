---
title: 设备管理器问题代码
description: 设备管理器问题代码
ms.assetid: d08c3dd1-ab2e-4ce6-8bf7-9634c0a5be1f
keywords:
- And 插即用 (PnP) 设备管理器问题代码
- 设备管理器问题代码
- CM_PROB_XXX
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: afa8b4fb0a8e88d71b3e8fe56cee8acf79bb0f84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541693"
---
# <a name="device-manager-problem-codes"></a>设备管理器问题代码


当设备有问题时，设备管理器将标记具有一个黄色感叹号 （！） 的设备。 问题代码是在窗体 CM\_PROB\_*XXX*和标头文件 cfg.h 中定义。 最重要的此处所述，以及其映射到[设备节点状态标志](device-node-status-flags.md)。 有关更全面的列表，请参阅[设备管理器错误消息](../install/device-manager-error-messages.md)。

<span id="Code_1__CM_PROB_NOT_CONFIGURED_"></span><span id="code_1__cm_prob_not_configured_"></span><span id="CODE_1__CM_PROB_NOT_CONFIGURED_"></span>**代码 1 (CM\_PROB\_不\_已配置)**  
表示设备未安装，并且之前未安装。 (对应于 DNF\_不\_已配置。)

<span id="Code_10__CM_PROB_FAILED_START_"></span><span id="code_10__cm_prob_failed_start_"></span><span id="CODE_10__CM_PROB_FAILED_START_"></span>**代码 10 (CM\_PROB\_失败\_开始)**  
指示设备未启动出于某种原因，但 I/O 管理器尝试启动使用一组资源。 (对应于 DNF\_启动\_失败。)

<span id="Code_12__CM_PROB_NORMAL_CONFLICT_"></span><span id="code_12__cm_prob_normal_conflict_"></span><span id="CODE_12__CM_PROB_NORMAL_CONFLICT_"></span>**代码 12 (CM\_PROB\_正常\_冲突)**  
指示没有足够的资源来启动此设备。 (对应于 DNF\_不足\_资源。)

<span id="Code_14__CM_PROB_NEED_RESTART_"></span><span id="code_14__cm_prob_need_restart_"></span><span id="CODE_14__CM_PROB_NEED_RESTART_"></span>**代码 14 (CM\_PROB\_需要\_重新启动)**  
指示用户模式重新配置设备，必须重新启动，以使更改生效。 (对应于 DNF\_需要\_重新启动。)

<span id="Code_18__CM_PROB_REINSTALL_"></span><span id="code_18__cm_prob_reinstall_"></span><span id="CODE_18__CM_PROB_REINSTALL_"></span>**Code 18 (CM\_PROB\_REINSTALL)**  
指示设备需要安装和以前已安装。 (对应于 DNF\_重新安装。)

<span id="Code_21__CM_PROB_WILL_BE_REMOVED_"></span><span id="code_21__cm_prob_will_be_removed_"></span><span id="CODE_21__CM_PROB_WILL_BE_REMOVED_"></span>**代码 21 (CM\_PROB\_将\_BE\_已删除)**  
指示用户模式下卸载此设备。 (对应于 DNF\_会\_BE\_已删除。)

<span id="Code_22__CM_PROB_DISABLED_"></span><span id="code_22__cm_prob_disabled_"></span><span id="CODE_22__CM_PROB_DISABLED_"></span>**代码 22 (CM\_PROB\_已禁用)**  
指示设备已被禁用。 (对应于 DNF\_已禁用。)

<span id="Code_28__CM_PROB_FAILED_INSTALL_"></span><span id="code_28__cm_prob_failed_install_"></span><span id="CODE_28__CM_PROB_FAILED_INSTALL_"></span>**代码 28 (CM\_PROB\_失败\_安装)**  
指示安装失败且是为此设备，选择任何驱动程序，尽管内核没有报告问题 (并且没有任何 DNF\_XXX 匹配此问题)。 此问题可能是尚未具有 INF 文件载入系统设备 （ISA 计时器、 ISA RTC、 RAM 内存等） 的结果。

<span id="Code_31__CM_FAILED_ADD_"></span><span id="code_31__cm_failed_add_"></span><span id="CODE_31__CM_FAILED_ADD_"></span>**代码 31 (CM\_失败\_添加)**  
指示设备未添加。 可能包括失败的原因： 驾**AddDevice**例程返回了错误，没有为设备注册表中列出的服务，没有列出，多个服务或无法加载控制驱动程序。 (对应于 DNF\_添加\_失败。)

 

 





