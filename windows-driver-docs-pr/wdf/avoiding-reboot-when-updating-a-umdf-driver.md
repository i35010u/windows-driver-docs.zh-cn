---
title: 更新 UMDF 驱动程序时避免重启
description: 更新 UMDF 驱动程序时避免重启
ms.assetid: B5321732-50FD-4719-BBD0-F0A3BE1EE532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14c9be629dc163a044f424f10c0813bf4084f21b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184329"
---
# <a name="avoiding-reboot-when-updating-a-umdf-driver"></a>更新 UMDF 驱动程序时避免重启


若要在更新 UMDF 驱动程序时避免需要重新启动，请在驱动程序的 INF 文件中的[**CopyFiles 指令**](../install/inf-copyfiles-directive.md)中指定**COPYFLG \_ in \_ USE \_ RENAME**标志，如以下示例中所示：

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

