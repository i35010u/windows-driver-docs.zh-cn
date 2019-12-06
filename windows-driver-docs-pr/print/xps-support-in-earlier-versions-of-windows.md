---
title: 早期 Windows 版本中的 XPS 支持
description: 早期 Windows 版本中的 XPS 支持
ms.assetid: e13b43f5-e926-404d-9f76-c2dfef6e0637
keywords:
- XPSDrv 打印机驱动程序 WDK，早期 Windows 版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b291ac69a78f7e464b850f0b4fb4ef8004ba4b9a
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881921"
---
# <a name="xps-support-in-earlier-versions-of-windows"></a>早期 Windows 版本中的 XPS 支持

除了 Windows Vista 以外，Microsoft Windows Server 2003 和 Windows XP 上还支持通过 Microsoft WinFX 运行时组件3.0 使用基于 XPS 的技术。 XPS 打印将在各种操作系统上适用于点和打印方案。

按以下方式提供对 Windows Server 2003 和 Windows XP 的支持：

- Win32 和 Windows Presentation Foundation （WPF）应用程序的输出透明转换。 尽管在 Win32 和 Windows Presentation Foundation （WPF）应用程序之间，呈现输出差别很大，但 XPSDrv 驱动程序模型使这两种应用程序类型可以打印到单个驱动程序。 用于打印的输出在应用程序类型和驱动程序类型之间进行适当地转换，从而在 Win32 和 WPF 应用程序之间实现完全支持矩阵，这些应用程序可打印到基于 GDI 和基于 XPS 的打印机。 XPSDrv 基础结构还可在 Windows Server 2003 和 Windows XP 中使用。

- 一致的筛选器管道模型。 Windows Vista、Windows Server 2003 和 Windows XP 上的筛选器管道支持用于筛选器、插件模型、管道配置文件和事件日志记录的相同接口。 有一些不同之处，包括更低版本 Windows 中的通知支持。 对于 Windows Vista，呈现筛选器可以完全控制通知，并且可以发送有关筛选器正在处理的任何类型 "部件" 的通知（即文档、页面、字体、图像等）。 对于早期版本 Windows 中的可缩放使用者，通知仅发生在页面边界。

- 基于 XPS 的打印处理器。 对于 Windows Server 2003 和 Windows XP，可以使用基于 XPS 的打印处理器来启用 XPSDrv。 基于 XPS 的打印处理器承载 XPSDrv 驱动程序，并与这些操作系统上的现有后台处理程序通信。 某些 XPS 打印路径功能只能在 Windows Vista 上使用，因此，XPSDrv 驱动程序必须能够在早期版本的 Windows 上正常降级。

有关 XPS 的详细信息，请下载[XML 纸张规范概述](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)。
