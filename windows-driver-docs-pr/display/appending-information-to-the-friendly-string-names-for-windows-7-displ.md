---
title: 将信息追加到 Windows 7 的显示器驱动程序友好名称
description: 描述你必须将其附加到 Windows 7 的显示器驱动程序的友好字符串名称的信息。
ms.assetid: 8c65f3d9-6f4c-49e9-a9b2-2689d83a181c
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3541b8030ca6be161a7275aaf63bcd078387d0d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545510"
---
# <a name="appending-information-to-the-friendly-string-names-for-windows-7-display-drivers"></a>将信息追加到 Windows 7 的显示器驱动程序的友好字符串名称


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

图形适配器的友好名称是在每个 Windows 7 的框中显示驱动程序 INF 中必需的可本地化的字符串名称。 上的部分[追加到友好字符串名称的图形适配器的信息](appending-information-to-the-friendly-string-names-of-graphics-adapter.md)描述必须追加的 Windows 显示器驱动程序模型 (WDDM) 的信息和[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)。 对于针对 Windows 7 进行了优化的 WDDM，必须将追加"(Microsoft Corporation 的 WDDM 1.1 版)":

```cpp
New Driver Model Foo Device Name (Microsoft Corporation - WDDM v1.1)
```

图形适配器的友好名称后面附有文本指定驱动程序使用的 WDDM 版本。

 

 





