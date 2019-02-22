---
title: QueryDisplayConfig 摘要和方案
description: QueryDisplayConfig 摘要和方案
ms.assetid: a556b3d7-3cac-49b1-99db-7ce8a844a8a8
keywords:
- 连接显示 WDK Windows 7 显示 QueryDisplayConfig 在 CCD Api
- 连接显示 WDK Windows Server 2008 R2 显示 QueryDisplayConfig 在 CCD Api
- 配置显示 WDK Windows 7 显示 QueryDisplayConfig 在 CCD Api
- 配置显示 WDK Windows Server 2008 R2 显示 QueryDisplayConfig 在 CCD Api
- CCD 概念 WDK Windows 7 显示 QueryDisplayConfig
- CCD 概念 WDK Windows Server 2008 R2 显示 QueryDisplayConfig
- QueryDisplayConfig WDK Windows 7 显示
- QueryDisplayConfig WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8508853ad0d09c3aec79f8f16f853f96a6114d75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526682"
---
# <a name="querydisplayconfig-summary-and-scenarios"></a>QueryDisplayConfig 摘要和方案


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

以下部分汇总了如何使用调用方[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) CCD 函数，并提供了有关使用方案**QueryDisplayConfig**。

### <a name="span-idquerydisplayconfigsummaryspanspan-idquerydisplayconfigsummaryspanquerydisplayconfig-summary"></a><span id="querydisplayconfig_summary"></span><span id="QUERYDISPLAYCONFIG_SUMMARY"></span>QueryDisplayConfig Summary

可以使用调用方[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)枚举任何以下信息：

-   可使用当前集的各个路径的所有连接监视器。 然后，调用方可以组合来构造可能的拓扑的路径。

-   所有当前处于活动状态的路径。

-   活动路径因为凭据当前定义的一套连接显示在持久性数据库中。

-   源和目标模式以及在每个路径的基础上的方向、 缩放、 布局和连接器类型。

-   当前拓扑将映射到热键选项。

### <a name="span-idquerydisplayconfigscenariosspanspan-idquerydisplayconfigscenariosspanquerydisplayconfig-scenarios"></a><span id="querydisplayconfig_scenarios"></span><span id="QUERYDISPLAYCONFIG_SCENARIOS"></span>QueryDisplayConfig Scenarios

[**QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)在以下情况下调用：

-   显示控件面板小程序调用[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)控制面板首次启动时填充与当前的应用拓扑的控制面板中的用户界面。 当前的应用的拓扑中包含这些显示在其启用强制的投影。

-   显示控件面板小程序调用[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)枚举所有可能的路径来填充**多监视器**下拉列表框。

-   显示控制面板用户界面启动之前，热键调用[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)若要获取的 （即，克隆，内部、 外部或扩展） 的当前设置显示选项。

-   第三方应用程序可能调用[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)若要查询的一套连接显示在数据库中存储的当前设置。

 

 





