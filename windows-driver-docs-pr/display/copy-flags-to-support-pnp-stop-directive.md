---
title: 复制标志以支持 PnP 停止指令
description: 有关 Windows 显示器驱动程序模型 (WDDM) 以支持不需要重新启动的驱动程序升级需要插即用 (PnP) 停止指令的文件部分标志。
ms.assetid: 0D78350C-52D9-49D5-817D-2672F4A1D41A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f17147db56303194139b141f525e4c12935fee89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330635"
---
# <a name="copy-flags-to-support-pnp-stop-directive"></a>复制标志以支持 PnP 停止指令


有关 Windows 显示器驱动程序模型 (WDDM) 以支持不需要重新启动的驱动程序升级需要插即用 (PnP) 停止指令的文件部分标志。

**请注意**  这是仅为用户模式驱动程序二进制文件，而不适用于内核模式驱动程序入口必需的。

 

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

 

 





