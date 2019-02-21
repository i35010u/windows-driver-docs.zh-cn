---
title: SetDisplayConfig 摘要和方案
description: SetDisplayConfig 摘要和方案
ms.assetid: f9bce5d4-b511-475c-8e0a-eb60765a3326
keywords:
- 连接显示 WDK Windows 7 显示 SetDisplayConfig 在 CCD Api
- 连接显示 WDK Windows Server 2008 R2 显示 SetDisplayConfig 在 CCD Api
- 配置显示 WDK Windows 7 显示 SetDisplayConfig 在 CCD Api
- 配置显示 WDK Windows Server 2008 R2 显示 SetDisplayConfig 在 CCD Api
- CCD 概念 WDK Windows 7 显示 SetDisplayConfig
- CCD 概念 WDK Windows Server 2008 R2 显示 SetDisplayConfig
- SetDisplayConfig WDK Windows 7 显示
- SetDisplayConfig WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e66eda4461096c81156dfa7b8f97e290acce7903
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519457"
---
# <a name="setdisplayconfig-summary-and-scenarios"></a>SetDisplayConfig 摘要和方案


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

以下部分汇总了如何使用调用方[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533) CCD 函数，并提供了有关使用方案**SetDisplayConfig**。

### <a name="span-idsetdisplayconfigsummaryspanspan-idsetdisplayconfigsummaryspansetdisplayconfig-summary"></a><span id="setdisplayconfig_summary"></span><span id="SETDISPLAYCONFIG_SUMMARY"></span>SetDisplayConfig 摘要

可以使用调用方[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)应用以及其他显示设置拓扑。 也就是说，可以使用调用方**SetDisplayConfig**若要设置拓扑、 布局、 方向、 纵横比，位深度，依次类推。 可以使用调用方**SetDisplayConfig**来执行以下操作：

-   设置源和目标的特定的拓扑。

-   定义布局、 方向和缩放系数以及每个路径的源和目标模式。

-   在应用的显示设置时，更新数据库。

-   测试是否可能通过使用枚举的路径已构造的特定的拓扑。

-   直接将应用从数据库映射到四个选项之一从热键的最后一个已知的设置。

-   启用强制的投影的目标。

-   调用新操作系统的最佳模式逻辑。

### <a name="span-idsetdisplayconfigscenariosspanspan-idsetdisplayconfigscenariosspansetdisplayconfig-scenarios"></a><span id="setdisplayconfig_scenarios"></span><span id="SETDISPLAYCONFIG_SCENARIOS"></span>SetDisplayConfig 方案

[**SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)在以下情况下调用：

-   显示控件面板小程序调用[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)若要测试所有可能的选项来填充**多监视器**下拉列表框。

-   显示控件面板小程序调用[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)将用户从下拉列表菜单中选择该设置。

-   显示控件面板小程序调用[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)以便将用户选择了从用户界面的设置。 这些设置包括解析、 布局、 方向、 缩放、 主、 位深度，并刷新频率。

-   显示用户进行选择后，热键调用[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)应用从持久性数据库的相应设置。

-   控制面板用户下的任务接口调用[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)应用适当的设置基于任务的类型。

-   显示控件面板小程序调用[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)启动或停止特定目标上强制的投影。

 

 





