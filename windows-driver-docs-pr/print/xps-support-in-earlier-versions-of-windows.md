---
title: 早期 Windows 版本中的 XPS 支持
description: 早期 Windows 版本中的 XPS 支持
ms.assetid: e13b43f5-e926-404d-9f76-c2dfef6e0637
keywords:
- XPSDrv 的打印机驱动程序 WDK，早期 Windows 版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4a85f89a820de51e585083c821a048df876f0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355128"
---
# <a name="xps-support-in-earlier-versions-of-windows"></a>早期 Windows 版本中的 XPS 支持


除 Windows Vista 中，在 Microsoft Windows Server 2003 和 Windows XP 通过 Microsoft WinFX 运行时组件 3.0 还支持基于 XPS 的技术。 XPS 打印将入点工作并输出使用这些操作系统的方案。

按以下方式提供对 Windows Server 2003 和 Windows XP 的支持：

-   Win32 和 Windows Presentation Foundation (WPF) 应用程序的输出的透明转换。 尽管呈现输出 Win32 和 Windows Presentation Foundation (WPF) 应用程序之间明显不同，但 XPSDrv 驱动程序模型，这两种应用程序类型输出到单个驱动程序。 用于打印的输出是相应地转换之间的应用程序类型和驱动程序类型，使打印到基于 GDI 的和基于 XPS 的打印机的 Win32 和 WPF 应用程序之间的完全支持矩阵。 XPSDrv 基础结构也是可在 Windows Server 2003 和 Windows XP 中使用。

-   一致的筛选器管道模型。 筛选器管道在 Windows Vista、 Windows Server 2003 和 Windows XP 支持的筛选器、 插件模型中，管道配置文件和事件日志记录相同的接口。 有一些区别，但在早期版本的 Windows 包括减少了的支持的通知。 适用于 Windows Vista 呈现筛选器有完全控制通知并可以发送通知"部分"筛选器处理任何类型 （即文档、 页、 字体、 图像，等）。 在早期版本的 Windows 的可缩放的使用者，通知发生这种情况仅在页边界。

-   基于 XPS 的打印处理器。 对于 Windows Server 2003 和 Windows XP 中，没有启用 XPSDrv 基于 XPS 的打印处理器。 基于 XPS 的打印处理器承载 XPSDrv 驱动程序，并与这些操作系统上的现有后台处理程序进行通信。 XPS 打印路径的某些功能是仅在 Windows Vista 上可用，因此 XPSDrv 驱动程序必须能够在早期版本的 Windows 正常降级。

有关 XPS 的详细信息，请下载[XML 纸张规范概述](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)。
