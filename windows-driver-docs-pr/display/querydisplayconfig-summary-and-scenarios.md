---
title: QueryDisplayConfig 摘要和方案
description: QueryDisplayConfig 摘要和方案
keywords:
- 连接显示 WDK Windows 7 显示、CCD Api、QueryDisplayConfig
- 连接显示 WDK Windows Server 2008 R2 display、CCD Api、QueryDisplayConfig
- 配置显示 WDK Windows 7 显示、CCD Api、QueryDisplayConfig
- 配置显示 WDK Windows Server 2008 R2 display、CCD Api、QueryDisplayConfig
- CCD 概念 WDK Windows 7 显示，QueryDisplayConfig
- CCD 概念 WDK Windows Server 2008 R2 显示，QueryDisplayConfig
- QueryDisplayConfig WDK Windows 7 显示
- QueryDisplayConfig WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 197cf421f0d0e4708082aba09a6df16b18ad770a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839581"
---
# <a name="querydisplayconfig-summary-and-scenarios"></a>QueryDisplayConfig 摘要和方案


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

以下部分概述了调用方如何使用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) CCD 函数并提供使用 **QueryDisplayConfig** 的方案。

### <a name="span-idquerydisplayconfig_summaryspanspan-idquerydisplayconfig_summaryspanquerydisplayconfig-summary"></a><span id="querydisplayconfig_summary"></span><span id="QUERYDISPLAYCONFIG_SUMMARY"></span>QueryDisplayConfig 摘要

调用方可以使用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) 来枚举以下任何信息：

-   当前连接的监视器集可能具有的所有单个路径。 然后，调用方可以组合路径来构造可能的拓扑。

-   当前处于活动状态的所有路径。

-   当前在持久性数据库中为一组连接的显示定义的活动路径。

-   源和目标模式，以及基于每个路径的方向、缩放、布局和连接器类型。

-   当前拓扑映射到的热键选项。

### <a name="span-idquerydisplayconfig_scenariosspanspan-idquerydisplayconfig_scenariosspanquerydisplayconfig-scenarios"></a><span id="querydisplayconfig_scenarios"></span><span id="QUERYDISPLAYCONFIG_SCENARIOS"></span>QueryDisplayConfig 方案

在以下情况下，将调用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) ：

-   当控制面板首次启动时，显示控制面板小程序会调用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) 来向控制面板的用户界面填充当前已应用的拓扑。 当前应用的拓扑包括启用强制投影时所显示的拓扑。

-   显示控制面板小程序调用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) 来枚举所有可能的路径，以填充 **multimon** 下拉框。

-   在开始 "控制面板" 用户界面之前，"显示" 热键会调用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) 来获取显示选项 (即，当前设置的、克隆、内部、外部或扩展) 。

-   第三方应用程序可以调用 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) ，以查询存储在数据库中的连接显示集的当前设置。

 

