---
title: 将信息追加到图形适配器友好的字符串名称
description: 必须将信息追加到的图形适配器的字符串名称。
ms.assetid: 660104ba-b082-407b-afdc-3e02f4c3d087
keywords:
- INF 文件 WDK 显示、 友好的字符串名称
- 友好的字符串名称 WDK 显示
- 图形适配器字符串 WDK 显示的名称
- 将 WDK 显示的字符串名称追加到图形适配器
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: a2828317136a7c3be2b23310a2b28f59778f7b2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525125"
---
# <a name="appending-information-to-the-friendly-string-names-of-graphics-adapters"></a>将信息追加到的图形适配器的友好字符串名称


必须将信息追加到的图形适配器的字符串名称。 此信息取决于适配器的驱动程序将写入到显示器驱动程序模型：

必须为 Windows 2000 的显示器驱动程序模型中，追加"(Microsoft Corporation)":

```cpp
XDDM Foo Device Name (Microsoft Corporation)
```

有关 Windows 显示器驱动程序模型 (WDDM)，您必须将追加"(Microsoft Corporation 的 WDDM)":

```cpp
New Driver Model Foo Device Name (Microsoft Corporation - WDDM)
```

有关详细信息*字符串*部分以及 *%strkey%* INF 中，在其他位置指定的令牌的更多信息参见[ **INF 字符串部分**](https://msdn.microsoft.com/library/windows/hardware/ff547485).

 

 





