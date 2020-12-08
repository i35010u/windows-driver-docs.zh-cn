---
title: 使用主题清单
description: 使用主题清单
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ddfee7bdc00be6073d3b3853f0195f70c56c50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785977"
---
# <a name="using-theme-manifests"></a>使用主题清单


如果将主题清单添加到适用于 Windows XP 的打印驱动程序，则可以确保驱动程序中的用户界面元素与 Windows XP 视觉样式匹配。

Windows XP 中的视觉样式是 Shell 公共控件 ( # A0，版本 6.0) 的更改的结果。 此版本几乎完全向后兼容5.0 版。 但是，当驱动程序在版本6.0 下运行时，为版本5.0 编写的驱动程序可能会出现一些问题。 为了避免此类问题，打印系统不会强制驱动程序使用版本 6.0 Comctl32.dll。 有关主题清单的示例，请 \\ 参阅 \\ \\ oemdll \\ 中的 src print ThemeUI \\ ThemeUI。

如果你将主题清单添加到指定依赖版本6的 Comctl32.dll 的依赖项，则它将在 Windows XP 及更高版本的操作系统版本以及 Windows 2000 上正常工作。 Windows 2000 忽略清单;因此，任何使用激活上下文都将正常失败。 请注意，由于 Comctl32.dll 版本5.0 不包含在全局程序集缓存中 (GAC) ，因此，指定此版本的 DLL 的依赖项的清单将中断组件。 在这种情况下，在尝试加载 Comctl32.dll 时，对 Win32 API **LoadLibrary** 的调用将失败。

应用程序可以具有全局 (或应用程序) 清单。 如果此全局清单包含使用 Comctl32.dll 版本6.0 的重定向，则会强制应用程序创建的所有 UI 使用同一主题。 这样做的一个结果是，无论驱动程序清单中是否存在任何 Comctl32.dll 重定向，使用全局清单从应用程序启动的打印机驱动程序都可能被强制使用 Comctl32.dll 版本6.0。

有关清单和程序集、激活上下文、独立应用程序和并行程序集共享的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




