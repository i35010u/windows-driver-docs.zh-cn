---
title: 设备管理器问题代码
description: 设备管理器问题代码
ms.assetid: d08c3dd1-ab2e-4ce6-8bf7-9634c0a5be1f
keywords:
- 即插即用 (PnP) ，设备管理器问题代码
- 设备管理器问题代码
- CM_PROB_XXX
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51790094df66ddf672394464991801c34c14c0c4
ms.sourcegitcommit: ad40820e3b3f66f9efcc14f8a00cc100fe0c6994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2020
ms.locfileid: "91620404"
---
# <a name="device-manager-problem-codes"></a>设备管理器问题代码


如果设备出现问题，设备管理器用黄色感叹号 (！ ) 标记设备。 问题代码的形式为 CM \_ PROB \_ *XXX* ，并在头文件 cfg 中定义。 此处介绍的是最重要的，它们及其到 [设备节点状态标志](device-node-status-flags.md)的映射。 有关更全面的列表，请参阅 [设备管理器错误消息](../install/device-manager-error-messages.md)。

<span id="Code_1__CM_PROB_NOT_CONFIGURED_"></span><span id="code_1__cm_prob_not_configured_"></span><span id="CODE_1__CM_PROB_NOT_CONFIGURED_"></span>**未配置代码 1 (CM \_ PROB \_ \_) **  
指示设备未安装并且以前未安装。  (对应于 " \_ 未 \_ 配置 DNF"。 ) 

<span id="Code_10__CM_PROB_FAILED_START_"></span><span id="code_10__cm_prob_failed_start_"></span><span id="CODE_10__CM_PROB_FAILED_START_"></span>**代码 10 (CM \_ PROB \_ \_ 启动失败) **  
表示设备由于某种原因而没有启动，但 i/o 管理器尝试使用一组资源启动它。  (对应于 DNF \_ 启动 \_ 失败。 ) 

<span id="Code_12__CM_PROB_NORMAL_CONFLICT_"></span><span id="code_12__cm_prob_normal_conflict_"></span><span id="CODE_12__CM_PROB_NORMAL_CONFLICT_"></span>**代码 12 (CM \_ PROB \_ 常规 \_ 冲突) **  
指示没有足够的资源来启动此设备。  (对应于 DNF \_ \_ 资源不足。 ) 

<span id="Code_14__CM_PROB_NEED_RESTART_"></span><span id="code_14__cm_prob_need_restart_"></span><span id="CODE_14__CM_PROB_NEED_RESTART_"></span>**代码 14 (CM \_ PROB \_ 需要 \_ 重启) **  
指示用户模式重新配置了设备，并且需要重新启动才能使更改生效。  (对应 DNF \_ 需要 \_ 重新启动。 ) 

<span id="Code_18__CM_PROB_REINSTALL_"></span><span id="code_18__cm_prob_reinstall_"></span><span id="CODE_18__CM_PROB_REINSTALL_"></span>**代码 18 (CM \_ PROB \_ 重新安装) **  
指示设备需要安装并已安装。  (对应于 DNF \_ 重新安装。 ) 

<span id="Code_21__CM_PROB_WILL_BE_REMOVED_"></span><span id="code_21__cm_prob_will_be_removed_"></span><span id="CODE_21__CM_PROB_WILL_BE_REMOVED_"></span>**将删除代码 21 (CM \_ PROB \_ \_ \_) **  
指示已卸载此设备的用户模式。  (\_ 将删除对应的 \_ DNF \_ 。 ) 

<span id="Code_22__CM_PROB_DISABLED_"></span><span id="code_22__cm_prob_disabled_"></span><span id="CODE_22__CM_PROB_DISABLED_"></span>**代码 22 (CM \_ PROB \_ 已禁用) **  
指示设备已禁用。  (对应于 \_ 禁用的 DNF。 ) 

<span id="Code_28__CM_PROB_FAILED_INSTALL_"></span><span id="code_28__cm_prob_failed_install_"></span><span id="CODE_28__CM_PROB_FAILED_INSTALL_"></span>**代码 28 (CM \_ PROB \_ \_ 安装失败) **  
指示安装失败并且没有为此设备选择驱动程序，尽管内核未报告问题 (并且 \_ 此问题) 没有 DNF XXX 匹配项。 此问题可能是由于以下原因引起的：板上的系统设备 (ISA 计时器、ISA RTC、RAM 内存等，因此还没有 INF 文件) 。

<span id="Code_31__CM_PROB_FAILED_ADD_"></span><span id="code_31__cm_failed_add_"></span><span id="CODE_31__CM_FAILED_ADD_"></span>**代码 31 (CM_PROB_FAILED_ADD) **  
指示未添加设备。 失败的原因可能包括：驱动程序的 **AddDevice** 例程返回了一个错误，在注册表中未列出该设备的服务，列出了多个服务，或者无法加载控制驱动程序。  (对应于 DNF \_ ADD \_ FAILED。 ) 

 

 





