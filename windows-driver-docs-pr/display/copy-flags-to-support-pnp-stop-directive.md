---
title: 复制标志以支持 PnP 停止指令
description: Windows 显示器驱动程序模型 (WDDM) 以支持不需要重新启动的驱动程序升级，即插即用 (PnP) 停止指令文件部分标志。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0001a3d3a685024fcab06a96a6d67c4808fa0694
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795013"
---
# <a name="copy-flags-to-support-pnp-stop-directive"></a>复制标志以支持 PnP 停止指令


Windows 显示器驱动程序模型 (WDDM) 以支持不需要重新启动的驱动程序升级，即插即用 (PnP) 停止指令文件部分标志。

**注意**  
这仅适用于用户模式驱动程序二进制文件，而不适用于内核模式驱动程序条目。

 

例如：

``` syntax
;
; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000             ; COPYFLG_IN_USE_TRY_RENAME
r200umd2.dll,,,0x00004000           ; COPYFLG_IN_USE_TRY_RENAME
```

 

 





