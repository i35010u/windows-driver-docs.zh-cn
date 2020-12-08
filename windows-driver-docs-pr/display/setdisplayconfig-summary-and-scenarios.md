---
title: SetDisplayConfig 摘要和方案
description: SetDisplayConfig 摘要和方案
keywords:
- 连接显示 WDK Windows 7 显示、CCD Api、SetDisplayConfig
- 连接显示 WDK Windows Server 2008 R2 display、CCD Api、SetDisplayConfig
- 配置显示 WDK Windows 7 显示、CCD Api、SetDisplayConfig
- 配置显示 WDK Windows Server 2008 R2 display、CCD Api、SetDisplayConfig
- CCD 概念 WDK Windows 7 显示，SetDisplayConfig
- CCD 概念 WDK Windows Server 2008 R2 显示，SetDisplayConfig
- SetDisplayConfig WDK Windows 7 显示
- SetDisplayConfig WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f18566b74476e4893a52230cc49ad3f4282dcc4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816809"
---
# <a name="setdisplayconfig-summary-and-scenarios"></a>SetDisplayConfig 摘要和方案


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下部分概述了调用方如何使用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) CCD 函数并提供使用 **SetDisplayConfig** 的方案。

### <a name="span-idsetdisplayconfig_summaryspanspan-idsetdisplayconfig_summaryspansetdisplayconfig-summary"></a><span id="setdisplayconfig_summary"></span><span id="SETDISPLAYCONFIG_SUMMARY"></span>SetDisplayConfig 摘要

调用方可以使用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 与其他显示设置一起应用拓扑。 也就是说，调用方可以使用 **SetDisplayConfig** 来设置拓扑、布局、方向、纵横比、位深度等。 调用方可以使用 **SetDisplayConfig** 来执行以下操作：

-   设置源和目标的特定拓扑。

-   定义每个路径的源和目标模式，以及布局、方向和比例因子。

-   应用显示设置时更新数据库。

-   测试是否可以使用枚举路径构造的特定拓扑。

-   直接应用从数据库映射到热键中四个选项之一的最后一个已知设置。

-   在目标上启用强制投影。

-   调用新的操作系统最佳模式逻辑。

### <a name="span-idsetdisplayconfig_scenariosspanspan-idsetdisplayconfig_scenariosspansetdisplayconfig-scenarios"></a><span id="setdisplayconfig_scenarios"></span><span id="SETDISPLAYCONFIG_SCENARIOS"></span>SetDisplayConfig 方案

在以下情况下，将调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) ：

-   显示控制面板小程序调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 来测试所有可能的选项，以填充 " **multimon** " 下拉框。

-   显示控制面板小程序调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 来应用用户从下拉菜单中选择的设置。

-   显示控制面板小程序调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 来应用用户从用户界面中选择的设置。 这些设置包括分辨率、布局、方向、缩放、主要、比特率和刷新频率。

-   用户做出选择后，显示热键将调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) ，以应用持久性数据库中的相应设置。

-   "控制面板" 用户界面下的任务调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 来应用适当的设置，该设置基于任务的类型。

-   显示控制面板小程序调用 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 来启动或停止特定目标上的强制投影。

 

