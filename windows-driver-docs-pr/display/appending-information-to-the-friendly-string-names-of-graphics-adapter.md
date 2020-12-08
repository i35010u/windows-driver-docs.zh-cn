---
title: 将信息追加到图形适配器友好字符串名称
description: 必须将信息追加到图形适配器的字符串名称。
keywords:
- INF 文件 WDK 显示，友好字符串名称
- 友好字符串名称 WDK 显示
- 图形适配器字符串名称 WDK 显示
- 追加到图形适配器字符串名称 WDK 显示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: cfe59f150d1a18bfc013f9a80649e35406056153
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810491"
---
# <a name="appending-information-to-the-friendly-string-names-of-graphics-adapters"></a>将信息追加到图形适配器的友好字符串名称


必须将信息追加到图形适配器的字符串名称。 此信息取决于适配器驱动程序写入的显示驱动程序模型：

对于 Windows 2000 显示器驱动程序模型，必须追加 " (Microsoft Corporation) "：

```cpp
XDDM Foo Device Name (Microsoft Corporation)
```

对于 Windows 显示驱动程序模型 (WDDM) ，必须追加 " (Microsoft Corporation-WDDM) "：

```cpp
New Driver Model Foo Device Name (Microsoft Corporation - WDDM)
```

有关在 INF 中其他地方指定的 *字符串* 部分和 *% strkey%* 令牌的详细信息，请参阅 [**inf 字符串部分**](../install/inf-strings-section.md)。

 

