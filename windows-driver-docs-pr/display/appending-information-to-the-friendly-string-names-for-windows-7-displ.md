---
title: 将信息追加到 Windows 7 显示驱动程序友好名称
description: 描述必须追加到 Windows 7 显示驱动程序的友好字符串名称的信息。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 65f675dc20116d8687a92582ea7e4159e119eb5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810489"
---
# <a name="appending-information-to-the-friendly-string-names-for-windows-7-display-drivers"></a>将信息附加到 Windows 7 显示驱动程序的友好字符串名称


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

图形适配器的友好名称是每个 Windows 7 内置显示器驱动程序的 INF 中所需的可本地化的字符串名称。 有关将 [信息追加到图形适配器的友好字符串名称](appending-information-to-the-friendly-string-names-of-graphics-adapter.md) 的部分介绍了必须为 Windows 显示驱动程序模型追加的信息 (WDDM) 和 [Windows 2000 显示驱动程序模型](windows-2000-display-driver-model-design-guide.md)。 对于用于 Windows 7 的 WDDM 优化，必须追加 " (Microsoft Corporation-WDDM v1.1) "：

```cpp
New Driver Model Foo Device Name (Microsoft Corporation - WDDM v1.1)
```

附加到图形适配器友好名称后面的文本指定驱动程序使用的 WDDM 版本。

 

 





