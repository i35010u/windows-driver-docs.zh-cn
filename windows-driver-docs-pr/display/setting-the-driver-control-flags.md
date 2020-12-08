---
title: 设置驱动程序控制标志
description: 设置驱动程序控制标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 233645fe60a2abe41eb562982d0a8606f69b6edc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826585"
---
# <a name="setting-the-driver-control-flags"></a>设置驱动程序控制标志


对于写入 Windows 显示 [驱动程序模型](mirror-drivers.md) (WDDM) 的所有驱动程序， **ExcludeFromSelect** 指令是必需的。

下面的示例演示如何将 **ExcludeFromSelect** 指令添加到 INF 文件的 **ControlFlags** 部分：

```inf
[ControlFlags]
ExcludeFromSelect=*
```

有关驱动程序控制标志的详细信息，请参阅 [**INF ControlFlags 部分**](../install/inf-controlflags-section.md)。

 

