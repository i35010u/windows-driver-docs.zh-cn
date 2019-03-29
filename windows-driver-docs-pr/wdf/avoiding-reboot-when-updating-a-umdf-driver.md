---
title: 更新 UMDF 驱动程序时避免重启
description: 更新 UMDF 驱动程序时避免重启
ms.assetid: B5321732-50FD-4719-BBD0-F0A3BE1EE532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e4edba5e0044bee795a5c3b65544cfb34806f89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566458"
---
# <a name="avoiding-reboot-when-updating-a-umdf-driver"></a>更新 UMDF 驱动程序时避免重启


若要避免需要重新启动更新 UMDF 驱动程序时，指定**COPYFLG\_IN\_使用\_重命名**标志中[ **CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)在驱动程序的 INF 文件中，在此示例中所示：

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

 





