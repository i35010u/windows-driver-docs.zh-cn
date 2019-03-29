---
title: 使用主题清单
description: 使用主题清单
ms.assetid: 8b3feb56-501b-4f35-937e-0be99338ae01
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95adc51aa8b632a387da2e6cb25cdb1782a2bdbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561748"
---
# <a name="using-theme-manifests"></a>使用主题清单


如果您添加到您的打印驱动程序适用于 Windows XP 主题清单，您可以确保该用户界面元素在您的驱动程序匹配的 Windows XP 视觉样式。

在 Windows XP 中的视觉样式是 Shell 公共控件 （Comctl32.dll，6.0 版） 中的更改的结果。 此版本是 5.0 版与几乎完全向后的兼容。 但是，某些问题可能与驱动程序版本 6.0 下运行时为 5.0 版编写的。 若要避免此类问题，打印系统不会强制驱动程序，以使用 Comctl32.dll 版本 6.0。 示例主题清单，请参阅\\src\\打印\\oemdll\\ThemeUI\\ThemeUI.Manifest WDK 中的。

如果主题清单添加到您指定的 Comctl32.dll 版本 6 依赖项的驱动程序时，它将正常工作以及 Windows 2000 上 Windows XP 和更高版本的操作系统版本。 Windows 2000 将忽略清单;因此任何使用的激活上下文的适当地将失败。 请注意由于 Comctl32.dll 版本 5.0 不包含在全局程序集缓存 (GAC) 中，指定此版本的 DLL 的依赖项的清单中断该组件。 在此情况下，调用 Win32 API **LoadLibrary**尝试加载 Comctl32.dll 时失败。

应用程序可以具有全局 （或应用程序） 的清单。 如果此全局清单包含使用 Comctl32.dll 版本 6.0 的重定向，这会强制所有用户界面的应用程序创建要使用相同的主题。 结果之一就是从全局清单的应用程序启动的驱动程序可能会被迫使用 Comctl32.dll 版本 6.0，而不考虑任何驱动程序清单中的 Comctl32.dll 重定向该打印机。

有关清单和程序集、 激活上下文，独立应用程序和共享的并行程序集的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




