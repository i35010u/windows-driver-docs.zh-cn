---
title: 更新 UMDF 驱动程序时避免重启
description: 更新 UMDF 驱动程序时避免重启
ms.assetid: B5321732-50FD-4719-BBD0-F0A3BE1EE532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d26ee878d1f74cedd88ce6c48d9e76b0fb45632
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379039"
---
# <a name="avoiding-reboot-when-updating-a-umdf-driver"></a>更新 UMDF 驱动程序时避免重启


若要避免需要重新启动更新 UMDF 驱动程序时，指定**COPYFLG\_IN\_使用\_重命名**标志中[ **CopyFiles 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)在驱动程序的 INF 文件中，在此示例中所示：

```cpp
[VirtualSerial_Install.NT]
CopyFiles=UMDriverCopy
 
[UMDriverCopy]
Virtualserial.dll,,,0x00004000  ; COPYFLG_IN_USE_RENAME
```

 

 





