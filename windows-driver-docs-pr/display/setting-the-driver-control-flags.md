---
title: 设置驱动程序控制标志
description: 设置驱动程序控制标志
ms.assetid: cca51b9c-ce37-4efb-ab42-8eb62b25eb21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f1d2fa78d3796a64cc361439f369a19586d5827
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065998"
---
# <a name="setting-the-driver-control-flags"></a>设置驱动程序控制标志


对于写入 Windows 显示[驱动程序模型](mirror-drivers.md) (WDDM) 的所有驱动程序， **ExcludeFromSelect**指令是必需的。

下面的示例演示如何将 **ExcludeFromSelect** 指令添加到 INF 文件的 **ControlFlags** 部分：

```inf
[ControlFlags]
ExcludeFromSelect=*
```

有关驱动程序控制标志的详细信息，请参阅 [**INF ControlFlags 部分**](../install/inf-controlflags-section.md)。

 

