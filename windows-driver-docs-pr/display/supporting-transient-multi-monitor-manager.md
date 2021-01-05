---
title: 支持暂用多监视器管理器
description: 支持暂用多监视器管理器
keywords:
- 暂时性的多监视器管理器 WDK 显示
- TMM WDK 显示
- 克隆视图 WDK 显示
- 移动设备 WDK，TMM 支持
- 监视配置 WDK 显示，TMM 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2268c031aa5272b8696d3c261f9731b33f4bf1d
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812579"
---
# <a name="supporting-transient-multi-monitor-manager"></a>支持暂用多监视器管理器

暂时性的多监视器管理器是一项 Windows Vista 功能，可简化在移动计算机上的显示配置的设置。 TMM 可以将移动计算机显示 (例如，当检测到新的监视器时，便携式计算机显示) 到克隆视图中。 在台式计算机上禁用 TMM。 对于 Windows Vista，不存在应用程序可以调用来输入克隆视图的 GDI 函数。 硬件供应商必须继续使用自己的专有方法在台式计算机上输入克隆视图。 但是，硬件供应商应该实现并提供 [IViewHelper](/windows/win32/api/cloneviewhelper) COM 接口对象，以允许 TMM 在移动计算机上设置克隆-查看模式。

本部分包括：

[TMM 术语](tmm-terminology.md)

[IViewHelper Clone-View COM 对象的要求](requirements-of-an-iviewhelper-clone-view-com-object.md)

[使用 IViewHelper Clone-View COM 对象](using-an-iviewhelper-clone-view-com-object.md)

[处理监视器配置](handling-monitor-configurations.md)

[确定平台是移动平台还是桌面平台](determining-whether-a-platform-is-mobile-or-desktop.md)
