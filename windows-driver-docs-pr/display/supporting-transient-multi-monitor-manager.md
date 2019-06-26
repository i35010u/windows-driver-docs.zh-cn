---
title: 支持暂用多监视器管理器
description: 支持暂用多监视器管理器
ms.assetid: 5091fe00-76d9-4585-9ef0-4b5b7ab8bc06
keywords:
- 暂时多监视器 Manager WDK 显示
- TMM WDK 显示
- 克隆的视图 WDK 显示
- WDK 的移动设备、 TMM 支持
- 监视器配置 WDK 显示区域，TMM 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35d3ce0e1463f832fa04b3a5dbd9d24d83d69202
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361216"
---
# <a name="supporting-transient-multi-monitor-manager"></a>支持暂用多监视器管理器


暂时多监视器管理器是一种 Windows Vista 功能，简化了移动计算机上显示配置的设置。 TMM 可以放置到克隆视图移动计算机显示 （例如，便携式计算机显示器） 时检测到新的监视器。 TMM 桌面计算机上禁用。 对于 Windows Vista 中，应用程序可以调用输入克隆视图没有 GDI 函数。 硬件供应商必须继续使用他们自己专有的方法输入的台式计算机上克隆视图。 但是，硬件供应商应实现并提供[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)将允许 TMM 移动计算机上克隆视图模式设置的 COM 接口对象。

本部分包括：

[TMM 术语](tmm-terminology.md)

[IViewHelper 克隆视图 COM 对象的要求](requirements-of-an-iviewhelper-clone-view-com-object.md)

[使用 IViewHelper 克隆视图 COM 对象](using-an-iviewhelper-clone-view-com-object.md)

[处理监视器配置](handling-monitor-configurations.md)

[确定是否平台为移动或桌面](determining-whether-a-platform-is-mobile-or-desktop.md)

 

 





