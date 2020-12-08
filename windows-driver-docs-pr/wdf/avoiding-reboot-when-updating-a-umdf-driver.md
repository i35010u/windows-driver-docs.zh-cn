---
title: 更新 UMDF 驱动程序时避免重启
description: 更新 UMDF 驱动程序时避免重启
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1f3a5b168467d8d9c7bfb7e0ca7f9d871f5ad06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815787"
---
# <a name="avoiding-reboot-when-updating-a-umdf-driver"></a>更新 UMDF 驱动程序时避免重启


若要在更新 UMDF 驱动程序时避免需要重新启动，请在驱动程序的 INF 文件中的 [**CopyFiles 指令**](../install/inf-copyfiles-directive.md)中指定 **COPYFLG \_ in \_ USE \_ RENAME** 标志，如以下示例中所示：

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

