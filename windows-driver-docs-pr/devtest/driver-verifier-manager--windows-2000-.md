---
title: 驱动程序验证程序管理器 (Windows 2000)
description: 驱动程序验证程序管理器 (Windows 2000)
keywords:
- 驱动程序验证器管理器
- 验证程序实用工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8414d9cda2800aeaca136d5741c938330f273a6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839003"
---
# <a name="driver-verifier-manager-windows-2000"></a>驱动程序验证程序管理器 (Windows 2000)


## <span id="ddk_driver_verifier_manager_windows_2000__tools"></span><span id="DDK_DRIVER_VERIFIER_MANAGER_WINDOWS_2000__TOOLS"></span>


驱动程序验证程序管理器的 Windows 2000 版本具有五个单独的面板：

1.  " **驱动程序状态** " 屏幕显示加载和正在验证的驱动程序以及哪些驱动程序验证程序选项处于活动状态。 有关详细信息，请参阅 [查看驱动程序验证程序设置](viewing-driver-verifier-settings.md) 。

2.  **全局计数器** 屏幕显示与驱动程序验证程序的操作相关的统计信息。 尽管其中一些统计信息与特定的驱动程序验证程序选项有关，但会显示这些统计信息，而不考虑哪些选项处于活动状态。 有关详细信息，请参阅 [监视全局计数器](monitoring-global-counters.md) 。

3.  " **池跟踪** " 屏幕显示有关池分配的信息。 有关详细信息，请参阅 [监视各个计数器](monitoring-individual-counters.md) 。

4.  " **设置** " 屏幕用于激活和配置驱动程序验证程序的操作。 从此屏幕进行的更改将在下一次启动后生效。 请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md) 和 [选择要验证的驱动程序](selecting-drivers-to-be-verified.md) 以获取详细信息。

5.  " **可变设置** " 屏幕用于改变驱动程序验证程序的易失性操作。 从此屏幕进行的更改会立即生效。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md) 。

许多屏幕上都有 **刷新频率** 部分。 这用于控制在该屏幕上所显示的信息的更新频率。 **Low**、 **Medium** 和 **High** 指令驱动程序验证器分别每1、5或10秒刷新一次屏幕。 **手动** 禁用自动更新。 " **立即刷新** " 按钮会使屏幕立即刷新。

若要退出驱动程序验证器管理器，请使用 " **退出** " 按钮。 如果进行了任何更改，但未按相应的 " **应用** " 按钮，系统会询问你是否要保存所做的更改。

 

 





